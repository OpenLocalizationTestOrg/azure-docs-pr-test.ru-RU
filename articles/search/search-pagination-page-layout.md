---
title: "Результаты поиска toopage aaaHow в поиске Azure | Документы Microsoft"
description: "Разбивка на страницы в службе Поиск Azure, размещенной облачной службе поиска в Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Отображением результатов поиска toopage в поиске Azure
Эта статья содержит рекомендации о том, как toouse hello API REST службы поиска Azure tooimplement стандартные элементы поиска страница результатов, например общего числа, получение документа, порядок сортировки и навигации.

В каждом случае упомянутых ниже указываются параметры, связанные с страницы, задействованных или данные страницы результатов поиска tooyour с помощью hello [поиска документов](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour запросов, отправленных службой поиска Azure. Запросы включают команды GET, путь и параметры запроса, которые сообщают о запрашиваемом службы hello и как tooformulate hello ответа.

> [!NOTE]
> Допустимый запрос содержит несколько элементов, например URL-адрес службы и путь, HTTP-команду, `api-version` и т. д. Для краткости мы ограничиваются hello toohighlight примеры просто hello синтаксис, соответствующий toopagination. См. в разделе hello [API REST службы поиска Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) Дополнительные сведения о синтаксисе запроса.
> 
> 

## <a name="total-hits-and-page-counts"></a>Общее количество совпадений и страниц
Отображается общее количество результатов, возвращенных запросом, а затем их возвращения результатов небольшими фрагментами hello, является основной toovirtually все страницы поиска.

![][1]

В поиске Azure используйте hello `$count`, `$top`, и `$skip` tooreturn параметры этих значений. Hello примере показан образец запроса для всего попаданий, возвращаются в виде `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Получать документы в группах 15, а также показать Всего попаданий hello, начиная с первой страницы приветствия:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Разбивки на страницы результатов требуются оба `$top` и `$skip`, где `$top` указывает, сколько элементов tooreturn в пакете, и `$skip` указывает, сколько элементов tooskip. В hello следующий пример, каждой страницы отображаются hello рядом 15 элементы, обозначенном hello добавочной переходы в hello `$skip` параметра.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Макет
На странице результатов поиска может потребоваться tooshow эскиза, подмножество полей и страницей ссылку tooa полной версии продукта.

 ![][2]

В поиске Azure, можно использовать `$select` уточняющего запроса командой tooimplement это взаимодействие.

tooreturn подмножество полей для мозаичного макета:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Изображения и файлам мультимедиа не непосредственно для поиска и должны храниться в другой платформы хранения, больших двоичных объектов Azure, например хранилище tooreduce затраты. В документах и индекс hello определите поле, содержащее URL-адрес hello hello внешнего содержимого. Затем можно использовать поле hello как ссылку на изображение. изображение toohello Hello URL-адрес должен находиться в документе hello.

странице описания продукта для tooretrieve **onClick** события, используйте [поиск документов](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass в ключе документа tooretrieve hello hello. Тип данных Hello hello ключа является `Edm.String`. В данном примере это *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Сортировка по соответствию, оценке или цене
Часто порядки сортировки по умолчанию toorelevance, но не общие toomake альтернативный порядок сортировки рукой, чтобы клиентов можно быстро передвинуть существующие результаты в другом порядке rank.

 ![][3]

В поиске Azure сортировки основан на hello `$orderby` выражения для всех полей, которые индексируются как`"Sortable": true.`

Соответствие тесно связано с профилями оценки. Можно использовать hello оценка по умолчанию, которой зависит от порядка toorank анализа и статистики текста все результаты с более высокой оценкой переходом toodocuments с совпадением дополнительные или более строгое условие поиска.

Альтернативные сортировки обычно связаны с **onClick** события, обратный вызов метода tooa, создает hello порядок сортировки. Например, если взять этот элемент страницы:

 ![][4]

Необходимо создать метод, который принимает параметр сортировки hello выбран в качестве входного и возвращает упорядоченный список для hello условие, связанное с этого параметра.

 ![][5]

> [!NOTE]
> Оценка по умолчанию hello является достаточным для многих сценариев, рекомендуется вместо индексация релевантности пользовательский профиль повышения. Настраиваемый профиль оценки дает вида tooboost элементов, которые являются более эффективным tooyour бизнеса. Дополнительные сведения см. в статье [Add scoring profiles to a search index (Azure Search Service REST API)](http://msdn.microsoft.com/library/azure/dn798928.aspx) (Добавление профилей оценки в индекс поиска (REST API службы поиска Azure)). 
> 
> 

## <a name="faceted-navigation"></a>Фасетная навигация
Навигация в поиске распространено на странице результатов, часто находится на стороне hello или верхней части страницы. В Поиске Azure фасетная навигация обеспечивает самостоятельный поиск на основе предварительно заданных фильтров. Дополнительные сведения см. в статье [Как реализовать фасетную навигацию в службе поиска Azure](search-faceted-navigation.md).

## <a name="filters-at-hello-page-level"></a>Фильтры на уровне страницы приветствия
Если проекту решения выделенной службы поиска страниц для определенных типов содержимого (например, сетевой розничный приложение, имеющее отделов, перечисленные в начале hello hello страницы), можно вставить выражение фильтра, наряду с **onClick** tooopen событий на страницу в предварительно профильтрованном состояния. 

Можно отправлять фильтр с выражением поиска или без него. Например hello следующий запрос используется для фильтрации собственное имя, возвращая только те документы, которые соответствуют его.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Дополнительные сведения о выражениях `$filter` см. в статье [Search Documents (Azure Search Service REST API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) (Поиск документов (REST API службы поиска Azure)).

## <a name="see-also"></a>См. также
* [REST API службы поиска Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Операции с индексами](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Операции с документом.](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Поиск Azure: учебники, видеодемонстрации и примеры](search-video-demo-tutorial-list.md)
* [Фасетная навигация в службе поиска Azure](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
