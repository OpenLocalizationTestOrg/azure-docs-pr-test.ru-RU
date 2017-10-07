---
title: "Поиск журнала aaaRegular выражения в аналитику журнала OMS | Документы Microsoft"
description: "Можно использовать ключевое слово hello регулярных выражений в анализа журналов выполняет toohello фильтра hello результатах журналов tooa регулярного выражения в соответствии с.  Эта статья содержит hello синтаксис для этих выражений с несколько примеров."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>С помощью регулярных выражений toofilter журнала выполняет поиск в службе анализа журналов

[Поиск журнала](log-analytics-log-searches.md) позволяют tooextract сведения из репозитория hello анализа журналов.  [Критерии фильтра](log-analytics-search-reference.md#filter-expressions) позволяют toofilter hello результаты поиска hello, в соответствии с toospecific критериев.  Hello **RegEx** ключевое слово позволяет toospecify регулярное выражение для этого фильтра.  

Эта статья содержит сведения о синтаксисе регулярных выражений hello, используется службой аналитики журналов.

> [!NOTE]
> Регулярное выражение можно использовать только в полях с поддержкой поиска.  Дополнительные сведения о полях, поддерживающих поиск, см. в разделе **Типы полей** статьи [Поиск данных по журналам в Log Analytics](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Ключевое слово RegEx

Hello используйте следующий синтаксис hello toouse **RegEx** ключевое слово в поиске по журналам.  Можно использовать другие разделы в этой статье toodetermine hello синтаксис регулярного выражения hello сам hello.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Например, записи toouse tooreturn оповещение в регулярное выражение с типом *предупреждение* или *ошибки*, можно использовать следующие поиска журналов hello.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Частичные совпадения
Обратите внимание, что hello регулярное выражение должно соответствовать hello весь текст hello свойства.  При частичных совпадениях ни одна запись не будет возвращена.  Например, если выполняется tooreturn записей на компьютере с именем srv01.contoso.com, hello, выполнив поиск журналов будет **не** возвратит никаких записей.

    Computer=RegEx("srv..")

Это происходит потому hello только первая часть имени hello соответствует регулярному выражению hello.  Hello следующие два журнала будет результатов поиска записей с этого компьютера несовпадения hello полное имя.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Знаки
Укажите различные знаки.

| Character | Описание | Пример | Пример совпадений |
|:--|:--|:--|:--|
| a | Одному вхождению символа hello. | Computer=RegEx("srv01.contoso.com") | Srv01.contoso.com |
| . | Любой отдельный знак. | Computer=RegEx("srv...contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| a? | Ноль или одно вхождение символа hello. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>Srv01.contoso.com |
| a* | Ноль или несколько вхождений символа hello. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Один или несколько вхождений символа hello. | Computer=RegEx("srv01+.contoso.com") | Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Соответствует любому одиночному символу в квадратных скобках hello | Computer=RegEx("srv0[123].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Совпадение с символом в диапазоне hello.  Может содержать несколько диапазонов. | Computer=RegEx("srv0[1-3].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Ни один из hello символов в квадратных скобках hello | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Ни один из знаков hello в диапазоне hello. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Соответствует диапазону числовых знаков. | Computer=RegEx("srv[01-03].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| @ | Любая строка знаков. | Computer=RegEx("srv@.contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Несколько вхождений знака
Укажите несколько вхождений определенных знаков.

| Character | Описание | Пример | Пример совпадений |
|:--|:--|:--|:--|
| a{n} |  *n*вхождения символа hello. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*или несколько вхождений символа hello. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*слишком*m* hello символов. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Логические выражения
Выберите из нескольких значений.

| Character | Описание | Пример | Пример совпадений |
|:--|:--|:--|:--|
| &#124; | Логический оператор OR.  Возвращает результат, если есть совпадение в любом из выражений. | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | Предупреждение<br>Ошибка |
| & | Логический оператор AND.  Возвращает результат, если есть совпадение в обоих выражениях. | EventData=regex("(Security.\*&.\*success.\*)") | Аудит системы безопасности успешно выполнен |


## <a name="literals"></a>Литералы
Преобразуйте символы tooliteral специальные символы.  Сюда входят символы, которые предоставляют функциональные возможности такие как выражения tooregular?-\*^\[\]{}\(\)+\|. &.

| Character | Описание | Пример | Пример совпадений |
|:--|:--|:--|:--|
| \\ | Преобразует литерала tooa специальный символ. | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [Error] Файл не найден.<br>Error. Файл не найден. |


## <a name="next-steps"></a>Дальнейшие действия

* Ознакомьтесь с [входа выполняет](log-analytics-log-searches.md) tooview и анализировать данные в репозиторий hello анализа журналов.
