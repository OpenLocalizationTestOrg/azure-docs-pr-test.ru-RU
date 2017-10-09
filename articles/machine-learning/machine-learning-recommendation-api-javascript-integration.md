---
title: "Рекомендации по машинному обучению: интеграция JavaScript | Документация Майкрософт"
description: "Рекомендации по машинному обучению Azure — интеграция JavaScript — документация"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Рекомендации по машинному обучению Azure — интеграция JavaScript
> [!NOTE]
> Необходимо запустить с помощью службы Когнитивных рекомендации API hello вместо этой версии. Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует. Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.
> Дополнительные сведения о [toohello перенос новой Когнитивных службы](http://aka.ms/recomigrate)
> 
> 

В этом документе отображения как toointegrate сайта с использованием JavaScript. Hello JavaScript позволяет toosend получение данных события и рекомендации tooconsume после построения модели рекомендаций. Все операции, которые совершаются при помощи JS, можно выполнить непосредственно на сервере.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Общая информация
Интеграция веб-сайта с рекомендациями Azure ML выполняется в 2 этапа.

1. Отправка событий в рекомендации Azure ML. Это позволит toobuild модели рекомендаций.
2. Использование рекомендаций hello. После построения модели hello могут потреблять hello рекомендации. (В этом документе не объясняют, как прочитать toobuild модели, hello краткое руководство по tooget Дополнительные сведения о том, как).

<ins>Этап I</ins>

В hello первого этапа, можно вставить в HTML-страницы небольшой библиотека JavaScript, которая позволяет hello страницы toosend события, происходящие на HTML-странице hello в Azure ML рекомендации серверов (с помощью Data Market):

![Рисунок1][1]

<ins>Этап II</ins>

В hello второй этап, когда требуется tooshow hello рекомендации на странице приветствия выбирается один из следующих вариантов hello:

1. сервер (этап hello визуализации страницы) вызывает рекомендации tooget сервера рекомендации машинного Обучения Azure (с помощью Data Market). Hello результатов включать список идентификаторов элементов. Сервер должен tooenrich hello результаты с элементами hello метаданных (например, изображения, описание) и отправить создан браузера toohello страницы приветствия.

![Рисунок2][2]

2. hello другой вариант — toouse hello небольшой JavaScript файл из одного tooget этап простой список рекомендуемых элементов. Здесь полученные данные Hello экономичные, чем один hello в первом варианте hello.

![Рисунок3][3]

## <a name="2-prerequisites"></a>2. Предварительные требования
1. Создайте новую модель с помощью API-интерфейсы hello. В разделе hello краткое руководство о том, как toodo его.
2. Закодируйте &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt;, используя base64. (Это будет использоваться для hello обычной проверки подлинности tooenable hello JS кода hello toocall API-интерфейсы).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Отправка событий получения данных при помощи JavaScript
следующие шаги Hello упрощения отправлять события:

1. Включите в код библиотеку JQuery. Его можно загрузить из nuget в hello URL-адреса.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Включена библиотека hello скрипт рекомендаций Java из hello URL-адреса: http://aka.ms/RecoJSLib1
3. Инициализируйте библиотеку Azure ML рекомендаций с соответствующими параметрами hello.
   
     <script>AzureMLRecommendationsStart («<base64encoding of username:key>», «< model_id >"); </script> 
4. Отправки hello соответствующее событие. Раздел с подробными сведениями о всех типах событий см. ниже (пример события щелчка) <script> if (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Ограничения и поддержка браузеров
Данная реализация является справочной и представлена как есть. Она должна поддерживаться во всех основных браузерах.

### <a name="32----type-of-events"></a>3.2.    Тип событий
Существует 5 типов событий, которые поддерживает библиотеку hello: нажмите кнопку, щелкните рекомендацию, добавьте tooShop покупок, удалите из бюро покупок и покупки. Нет дополнительных событие, которое используется tooset hello пользовательский контекст входа.

#### <a name="321-click-event"></a>3.2.1. Событие "Щелчок"
Это событие должно использоваться всякий раз, когда пользователь щелкает элемент. Обычно в том случае, когда пользователь щелкает элемент открывается новая страница с hello сведения об элементе; на этой странице должна активироваться это событие.

Параметры

* event (строка, обязательный) — click.
* элемент (string, обязательные) — уникальный идентификатор элемента hello
* itemName (string, необязательно) — имя hello элемента hello
* itemDescription (string, необязательно) — описание hello элемента hello
* itemCategory (string, необязательно) — hello категорию элемента hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Или с дополнительными данными:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Событие "щелчок рекомендации"
Это событие должно использоваться всякий раз, когда пользователь щелкает элемент, который был получен из рекомендаций Azure ML в качестве рекомендованного элемента. Обычно в том случае, когда пользователь щелкает элемент открывается новая страница с hello сведения об элементе; на этой странице должна активироваться это событие.

Параметры

* event (строка, обязательный) — recommendationclick.
* элемент (string, обязательные) — уникальный идентификатор элемента hello
* itemName (string, необязательно) — имя hello элемента hello
* itemDescription (string, необязательно) — описание hello элемента hello
* itemCategory (string, необязательно) — hello категорию элемента hello
* начальные значения (массив строк, необязательно) - hello начальные значения, сформированных запросов рекомендацию hello.
* recoList (массив строк, необязательно) - hello результат запроса рекомендация hello, вызвавшего hello элемента, который был щелкнут.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Или с дополнительными данными:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Событие добавления товара в корзину
Это событие должно использоваться при hello пользователь добавлять элемент toohello Корзина для покупок.
Параметры

* event (строка, обязательный) — addshopcart.
* элемент (string, обязательные) — уникальный идентификатор элемента hello
* itemName (string, необязательно) — имя hello элемента hello
* itemDescription (string, необязательно) — описание hello элемента hello
* itemCategory (string, необязательно) — hello категорию элемента hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Событие удаления товара из корзины
Это событие следует использовать, когда пользователь hello удаляет элемент toohello корзину для покупок.

Параметры

* event (строка, обязательный) — removeshopcart.
* элемент (string, обязательные) — уникальный идентификатор элемента hello
* itemName (string, необязательно) — имя hello элемента hello
* itemDescription (string, необязательно) — описание hello элемента hello
* itemCategory (string, необязательно) — hello категорию элемента hello
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Событие покупки
Это событие можно использовать при hello пользователь приобрел свою корзину для покупок.

Параметры

* event (строка) — purchase.
* items ( Purchased[] ) — массив, содержащий запись для каждого приобретенного элемента.<br><br>
  Формат приобретенных элементов
  * элемент (строка) — уникальный идентификатор элемента hello.
  * count (целое число или строка) — количество приобретенных элементов.
  * Цена (число с плавающей запятой или строка) — необязательное поле - hello цена hello элемента.

Hello приведенном ниже примере показано покупки из 3 элементов (33, 34, 35) двух все заполнены поля (элемент, количество, цена) и второй (элемент 34) без цену.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Событие входа пользователя
Здравствуйте, Azure ML рекомендации библиотека создает и использовать куки-файла в порядке tooidentify события, полученные из браузера. В модели hello tooimprove порядок результатов Azure ML рекомендации обеспечивает tooset уникальный идентификатор пользователя, переопределяют hello использования файлов cookie.

Это событие можно использовать после узел tooyour входа пользователя hello.

Параметры

* event (строка) — userlogin.
* пользователь (строка) — уникальный идентификатор пользователя hello.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Использование рекомендаций с помощью JavaScript
Hello код, который использует hello рекомендации по некоторому событию JavaScript инициируется hello клиента веб-страницы. Hello рекомендация ответ включает hello рекомендуемые идентификаторы элементов, их имена и их оценки. Это наиболее toouse на стороне интеграции hello server следует сделать этот параметр только для отображения списка hello рекомендуемых элементов - более сложные обработки (например, добавление метаданных элемента hello).

### <a name="41-consume-recommendations"></a>4.1. Потребление рекомендаций
tooconsume рекомендации, необходимые tooinclude hello необходимые библиотеки JavaScript в страницу и toocall AzureMLRecommendationsStart. См. раздел 2.

tooconsume рекомендаций для одного или нескольких элементов требуется вызывается метод toocall: AzureMLRecommendationsGetI2IRecommendation.

Параметры

* элементы (массив строк) — один или несколько элементов tooget рекомендации. При использовании сборки Fbt здесь можно задать только один элемент.
* numberOfResults (целое число) — количество необходимых результатов.
* includeMetadata (логическое значение, необязательно) — Если задать too'true "Указывает, должны быть заполнены поля метаданных hello в результате hello.
* Функция обработки - функция, которая будет обрабатывать возвращаемые рекомендации hello. Hello данные возвращаются в виде массива:
  * item — уникальный идентификатор элемента.
  * name — имя элемента (если существует в каталоге).
  * rating — рейтинг рекомендации.
  * метаданные - строка, представляющая hello метаданных элемента hello

Пример: hello, следующий код запрашивает 8 рекомендации для элемента «64f6eb0d-947a-4c18-a16c-888da9e228ba» (и, не указывая includeMetadata - он неявно говорится, что метаданные не требуется), затем объединить результаты hello в буфер.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
