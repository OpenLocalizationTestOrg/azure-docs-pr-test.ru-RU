---
title: "aaaInteract с отчетами с помощью JavaScript API hello | Документы Microsoft"
description: "Power BI Embedded, взаимодействовать с отчетами с помощью JavaScript API hello"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Взаимодействие с отчетами Power BI, с помощью JavaScript API hello
включает Power BI JavaScript API Hello tooeasily можно внедрить Power BI с отчетами в приложения. С hello API приложений программного взаимодействия с различных отчетов элементы, такие как страницы и фильтры. Эти интерактивные возможности обеспечивают более полную интеграцию отчетов Power BI с приложениями.

Внедрение отчета Power BI в приложение с помощью iframe, размещенной в рамках приложения hello. Hello iframe действует как граница между приложением и hello отчета, как видно в hello после изображения. 

![Плавающий фрейм Power BI Embedded без интерфейса API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hello iframe делает hello, внедрение процесса намного проще, но без hello JavaScript API hello отчетов и приложение не может взаимодействовать друг с другом. Отсутствие взаимодействия может упростить кажется, что отчет hello не действительно является частью приложения hello. Hello отчетов и приложение действительно требуется toocommunicate назад и вперед как hello после изображения.

![Плавающий фрейм Power BI Embedded c интерфейсом API JavaScript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Hello Power BI JavaScript API позволяет toowrite кода, можно безопасно передать через границу iframe hello. Это позволяет tooprogrammatically вашего приложения выполнять действия в отчете и toolisten для событий из действия, настроенные пользователями в отчете hello.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Что можно делать с hello Power BI JavaScript API?
Hello JavaScript API можно управлять отчетами, перейдите toopages в отчете, фильтрации отчетов и обработки внедрение события. Hello следующей схеме показана структура hello hello API.

![Схема интерфейса API JavaScript службы Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Управление отчетами
Hello Javascript API позволяет toomanage поведение на уровне отчета и страницы приветствия:

* Безопасно внедрение определенный отчет Power BI в приложение — попробуйте hello [внедрить демонстрационного приложения](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Задание маркера доступа.
* Настройка отчетов hello
  * Включение и отключение панели фильтра hello и область навигации по страницам — попробуйте hello [обновить параметры демонстрационного приложения](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Настройки по умолчанию для страниц и фильтры - попытайтесь hello [демонстрационный набор значений по умолчанию](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Включение и выключение полноэкранного режима.

[Дополнительные сведения о внедрении отчетов.](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Перейдите toopages в отчете
Здравствуйте, enbales JavaScript API, вы toodiscover всех страниц в отчете и tooset hello текущей страницы. Повторите hello [навигации демонстрационное приложение](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Дополнительные сведения о навигации по страницам.](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Фильтрация данных в отчете
Hello JavaScript API предоставляет основные и расширенные возможности встроенные отчеты и страницы отчета фильтрации. Повторите hello [фильтрации демонстрационное приложение](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)и просмотрите некоторых вводных кода.  

#### <a name="basic-filters"></a>Базовые фильтры
Базовый фильтр помещается на уровне столбца или иерархии, содержит список значений tooinclude или исключить.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Расширенные фильтры
Расширенные фильтры использовать логический оператор hello и или или и принять одно или два условия, каждый из которых собственные оператор и значение. Поддерживаются такие условия:

* None
* LessThan;
* LessThanOrEqual;
* GreaterThan
* GreaterThanOrEqual;
* Содержит
* DoesNotContain;
* StartsWith;
* DoesNotStartWith;
* Is;
* IsNot;
* IsBlank;
* IsNotBlank.

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Дополнительные сведения о фильтрации.](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Обработка событий
В дополнение к этому toosending информацию в hello iframe, приложения могут также получать сведения о следующих событий, поступающих из hello iframe hello:

* внедрение;
  * загрузка;
  * error
* Отчеты
  * изменение страницы;
  * выбор данных (ожидается в ближайшее время).

[Дополнительные сведения об обработке событий.](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello Power BI JavaScript API ознакомьтесь с hello ссылкам:

* [Вики-сайт по интерфейсу API JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Справочник по объектным моделям](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Примеры
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Демонстрация в реальном времени](https://microsoft.github.io/PowerBI-JavaScript/demo/)

