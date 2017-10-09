---
title: "aaaAzure поиска многоязыковой | Документы Microsoft"
description: "Служба поиска Azure поддерживает 56 языков — для этого используются языковые анализаторы Lucene и технология Майкрософт для обработки естественных языков."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Создание индекса для многоязычных документов в поиске Azure
> [!div class="op_single_selector"]
>
> * [Портал](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing hello языковых анализаторов является так же легко, как свойство один параметр для поиска поля в определение индекса hello. Теперь можно выполнить этот шаг в портал hello.

Ниже приведены снимки экрана приветствия колонках портала Azure для службы поиска Azure, позволяют пользователям toodefine схему индекса. В этой колонке пользователи могут создавать все поля hello и задать свойство анализатора hello для каждого из них.

> [!IMPORTANT]
> Можно задать только анализатора языка во время определения поля, как в при при создании нового индекса hello основание, или при добавлении нового поля tooan существующий индекс. Убедитесь, что полностью указывать все атрибуты, включая hello анализатора, при создании поля hello. Не быть может tooedit атрибутами hello или изменить тип анализатора hello после сохранения изменений.
>
>

## <a name="define-a-new-field-definition"></a>Добавление определения нового поля
1. Войдите в toohello [портал Azure](https://portal.azure.com) и Привет открыть колонку службы поиска службы.
2. Нажмите кнопку **добавить индекс** в hello командной строке вверху hello toostart панели мониторинга службы hello новый индекс или откройте существующий индекс tooset анализатора на новые поля, которые вы добавляете tooan существующий индекс.
3. Появится колонки полей Hello, содержащее параметры для определения схемы hello hello индекса, в том числе вкладку анализатора hello используется для выбора анализатора языка.
4. В полях запустите определение поля, указание имени и типа данных hello и задания атрибутов toomark hello поле как полный текст для поиска, в результаты поиска, можно использовать в структурах навигации аспекта, извлекаемые сортируемого и т. д.
5. Прежде чем продолжить toohello следующее поле, откройте hello **анализатора** вкладки.

![][1]
*tooselect анализатора, откройте вкладку анализатора hello в колонке поля hello*

## <a name="choose-an-analyzer"></a>Выбор анализатора
1. Прокрутите toofind hello поле, которое вы определяете.
2. Если еще не помечен как поле hello как с возможностью поиска, нажмите кнопку toomark теперь флажок hello его как **доступный**.
3. Выберите hello анализатора области toodisplay hello список доступных анализаторов.
4. Выберите анализатор hello требуется toouse.

![][2]
*Выберите один из hello Поддерживаемые анализаторы для каждого поля*

По умолчанию все поддерживающие поиск поля используют hello [Lucene стандартный анализатор](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) которого не зависит от языка. tooview hello полный список поддерживаемых анализаторов см. в разделе [языковая поддержка в поиске Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Выбрав hello анализатора языка для поля, он будет использоваться при каждом запросе индексирования и поиска для этого поля. При выдаче запроса от нескольких полей с помощью различных анализаторов hello запрос будет обрабатываться независимо друг от друга hello правой анализаторы для каждого поля.

Многие веб- и мобильных приложений обслуживает пользователей земного шара hello, с использованием различных языков. Это возможно toodefine индекса для сценария, как в данном путем создания поля для каждого поддерживаемого языка.

![][3]
*Определение индекса с полем описания для каждого поддерживаемого языка*

Если известны языка hello hello агента, выполнение запроса, запрос поиска может быть tooa с областью конкретного поля, с помощью hello **searchFields** параметр запроса. Hello следующий запрос будет выполняться только для описания hello в польского языка:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Можно запросить индекс из портала hello, с помощью **обозреватель поиска** toopaste в toohello аналогичные запроса, которое показано выше. Поиск в обозревателе можно получить на панели команд hello в колонке службы hello. В разделе [запросить индекс поиска Azure на портале hello](search-explorer.md) подробные сведения.

Иногда hello языка hello агента, выполнение запроса не известно, в какой вариантов hello запрос может быть произведен от всех полей одновременно. При необходимости можно сделать какой-то язык предпочтительным, воспользовавшись [профилями оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx). В следующем примере hello совпадений, обнаруженных в описании hello на английском языке оцененные выше относительный toomatches в польский и французского языков:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Если вы разработчик .NET, обратите внимание, что можно настроить с помощью hello анализаторы языка [пакет SDK Azure Search .NET](http://www.nuget.org/packages/Microsoft.Azure.Search). последний выпуск Hello включает поддержку анализаторы языка Microsoft hello также.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
