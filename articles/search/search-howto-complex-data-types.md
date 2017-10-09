---
title: "aaaHow toomodel сложных типов данных в поиске Azure | Документы Microsoft"
description: "Вложенные или иерархические структуры данных можно моделировать в индексе Поиска Azure с помощью плоских наборов строк и типа данных \"Коллекции\"."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Как типы toomodel сложных данных в поиске Azure
Внешних наборов данных используется toopopulate индекс поиска Azure иногда содержат иерархические или вложенном вложенные структуры, которые не нарушают аккуратно в виде табличного набора строк. К примерам таких структур можно отнести несколько расположений и номеров телефонов для одного клиента, несколько цветов и размеров для одного SKU, несколько авторов на одну книгу и т. д. Моделирование условия, вы видите, эти структуры называется tooas *сложные типы данных*, *составные типы данных*, *составные типы данных*, или *статистические типы данных*, tooname несколько.

Сложные типы данных не поддерживаются изначально в поиске Azure, но проверенные решение включает два этапа выравнивание структуры hello и затем с помощью **коллекции** типа tooreconstitute hello внутренние структуры данных. Следование hello способ, описанный в этой статье позволяет содержимого toobe hello которой выполняется поиск, аспекта, фильтрация и сортировка.

## <a name="example-of-a-complex-data-structure"></a>Пример сложной структуры данных
Обычно данные hello рассматриваемой находится как JSON или XML-документов или элементов в хранилище NoSQL, таких как Azure Cosmos DB. Структурно запрос hello основанная на наличие нескольких дочерних элементов, которые требуется toobe поиска и фильтрации.  В качестве отправной точки для наглядного hello решение выполните hello следующий документ JSON, который содержит набор контакты в качестве примера.

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Хотя hello поля с именем «id», «name» и «компания» могут легко быть сопоставлены одному как поля в индекс поиска Azure, поле «расположение» hello содержит массив расположений, применения оба набора идентификаторов расположение, а также расположение описания. Учитывая, что поиск Azure не имеет тип данных, который поддерживает это, мы должны toomodel иначе это в поиске Azure. 

> [!NOTE]
> Этот метод также представлено Evans Кирк в записи блога [индексирования DocumentDB с поиском Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), который демонстрирует метод, называемый «обработки прозрачности hello данных», согласно которому будет иметь поле с именем `locationsID` и `locationsDescription` которые оба [коллекций](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массив строк).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Часть 1: Сведение hello массива в отдельные поля
toocreate индекс поиска Azure, который допустим для этого набора данных, создайте отдельные поля для вложенных подструктуре hello: `locationsID` и `locationsDescription` с типом данных [коллекций](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массив строк). В этих полях будет индексировать hello значения "1" и "2" в hello `locationsID` поля для значений John Smith "и" hello, "3" и "4" в hello `locationsID` для Jen Campbell.  

Данные в Поиске Azure будут выглядеть следующим образом: 

![пример данных, 2 строки](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Часть 2: Добавление поля коллекции в определение индекса hello
В схеме индекса hello hello определения полей может выглядеть аналогичный пример toothis.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Проверить режимы работы поиска и при необходимости расширить индекс hello
При условии, что индекс созданного hello hello загруженных данных, теперь можно проверить выполнение hello решения tooverify поиска запросов на hello набора данных. Каждое поле типа **Коллекция** должно поддерживать **поиск**, **фильтрацию** и **поиск с использованием фасетов**. Вы должны быть запросов может toorun как:

* Поиск всех лиц, которые работают на «Adventureworks штаб-квартире» hello.
* Получение числа hello количество пользователей, работающих в «Домашнего офиса».  
* Hello людей, которые работают на «Домашнего офиса» показано, какие офисов, они работают вместе с count hello людей в каждом местоположении.  

Где друг от друга, этот метод становится — при необходимости toodo поиск, который объединяет ИД расположения hello как, так и описание размещения hello. Например:

* Найти всех людей, работающих в главном офисе (значение Home Office) с идентификатором расположения 4.  

Если вы вспомните исходного содержимого hello выглядело следующим образом:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Однако теперь, когда был разделен hello данных в отдельные поля, у нас есть не может определить, если слишком относятся hello домашнего офиса для Jen Campbell`locationsID 3` или `locationsID 4`.  

toohandle в данном случае определение другого поля в индексе hello, объединяющее все данные hello в одну коллекцию.  В нашем примере мы называем это поле `locationsCombined` и будет разделить hello содержимое с `||` несмотря на то, что можно выбрать любой разделитель, которая будет уникальный набор символов для содержимого. Например: 

![пример данных, 2 строки с разделителем](./media/search-howto-complex-data-types/sample-data-2.png)

С помощью поля `locationsCombined` теперь можно разместить еще больше запросов, например:

* отображение числа людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4";  
* поиск людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4". 

## <a name="limitations"></a>Ограничения
Этот метод полезен в ряде сценариев, но не подходит в каждом случае.  Например:

1. Если у вас набор статических полей в типе сложных данных и возникла не toomap способом все возможные hello типами tooa одно поле. 
2. При обновлении hello вложенных объектов требуется некоторые дополнительные действия toodetermine точно, требующие обновления в индекс поиска Azure hello toobe

## <a name="sample-code"></a>Пример кода
Можно увидеть пример на tooindex сложных данных JSON настроек в поиске Azure и выполнять запросы через этот набор данных на этом [в репозитории GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Дальнейшие действия
[Голоса для собственная поддержка для сложных типов данных](https://feedback.azure.com/forums/263029-azure-search) на hello UserVoice поиска Azure страницы и укажите любые дополнительные входные данные, желательно нам tooconsider относительно реализации функций. Также можно войти toome непосредственно в Twitter с @liamca.

