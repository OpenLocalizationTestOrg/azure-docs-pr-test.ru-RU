---
title: "aaaMachine обучения рекомендации документации по API | Документы Microsoft"
description: "API рекомендации обучения машины документации по Azure для рекомендаций подсистемы, доступные в Microsoft Azure Marketplace hello."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Машинное обучение Azure: документация по интерфейсу API рекомендаций
> [!NOTE]
> Необходимо запустить с помощью службы Когнитивных рекомендации API hello вместо этой версии. Эта служба будет заменена Hello службы Когнитивных рекомендации и всех hello новых функций, которые будут реализованы существует. Она включает в себя новые возможности, такие как поддержка пакетной обработки, улучшенный обозреватель API, более четкое представление API, более согласованные процедуры регистрации и выставления счетов, и т. д.
> Дополнительные сведения о [toohello перенос новой Когнитивных службы](http://aka.ms/recomigrate)
> 
> 

В этом документе описываются интерфейсы API рекомендаций по Машинному обучению Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Общая информация
Данный документ содержит справочные материалы по интерфейсам API. Рекомендуется начать с документом «Azure рекомендация — быстрый запуск машинного обучения» hello.

Hello Azure машины обучения рекомендации API можно разделить на следующие логические группы hello:

* <ins>ограничения</ins> — ограничения API рекомендаций.
* <ins>общая информация</ins> — сведения об аутентификации, универсальном коде ресурса (URI) службы и управлении версиями.
* <ins>Модели Basic</ins> -API, которые позволяют toodo hello основных операций модели (например создание, обновление и удаление модели).
* <ins>Модели Дополнительно</ins> -API, которые позволяют tooget advanced анализу данных на модель hello.
* <ins>Модели бизнес-правила</ins> -API, которые позволяют бизнес-правила toomanage hello модели рекомендаций результатов.
* <ins>Каталог</ins> -API, которые позволяют toodo основных операций для каталога модели. Каталог содержит метаданные для элементов данных об использовании hello hello.
* <ins>Функция</ins> -интерфейсы API, позволяющие tooget аналитики на элемент в каталог hello и как toouse этой информации toobuild рекомендации более полезными.
* <ins>Данные об использовании</ins> -API, которые позволяют toodo основные операции с данными об использовании модели hello. Данные об использовании в базовой форме hello состоит из строки, содержащие пары &#60; userId &#62; &#60; itemId &#62;.
* <ins>Построение</ins> - API-интерфейсы, позволяющие tootrigger модели построение и выполнение основных операций, связанных toothis сборки. Инициировать сборку модели можно, получив значимые данные об использовании.
* <ins>Рекомендация</ins> -интерфейсы API, позволяющие tooconsume рекомендации после завершения построения hello модели.
* <ins>Данные пользователя</ins> -API, которые позволяют toofetch сведения о данных об использовании hello пользователя.
* <ins>Уведомления о</ins> -tooyour API-операции, связанные с API-интерфейсы, обеспечивающие tooreceive уведомления о проблемах. (Например, вы сообщаете использование данных с помощью получения данных и большинство hello событий ошибки обработки при выполнении. то вызывается сообщение об ошибке.

## <a name="2-limitations"></a>2) Ограничения
* Hello моделей для каждой подписки не более 10.
* Hello максимальное количество сборок на модели — 20.
* Максимальное количество элементов, содержащихся в каталоге для Hello составляет 100 000.
* Hello использования точек, которые хранятся не более 5 000 000 ~. Если новые будут отправлены или отмечены Hello старые будут удалены.
* Hello максимальный объем данных, которые могут отправляться в POST (например импорта каталога данных, импорт данных об использовании) — 200 МБ.
* Максимальное количество элементов, которые можно указать при получении рекомендации Hello — 150.

## <a name="3-apis---general-information"></a>3. Интерфейсы API: общие сведения
### <a name="31-authentication"></a>3.1. Аутентификация
Следуйте правилам hello Microsoft Azure Marketplace, связанные с проверкой подлинности. Hello marketplace поддерживает метод проверки подлинности Basic или OAuth либо hello.

### <a name="32-service-uri"></a>3.2. URI службы
Корень службы Hello URI для hello API-интерфейсов Azure машины обучения рекомендации [здесь.](https://api.datamarket.azure.com/amla/recommendations/v3/)

Hello полный URI службы представляется с помощью элементов hello спецификации OData.  

### <a name="33-api-version"></a>3.3. Версия API
Каждый вызов API будет, в конце hello параметр запроса с именем apiVersion, который следует задать too1.0.

### <a name="34-ids-are-case-sensitive"></a>3.4. Идентификаторы с учетом регистра
Идентификаторы, возвращенные любой hello API-интерфейсы, чувствительны к регистру и должны использоваться таким образом, при передаче в качестве параметров при последующих вызовах API. Например, регистр учитывается в идентификаторах моделей и каталогов.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Качество рекомендаций и неактивные элементы
### <a name="41-recommendation-quality"></a>4.1. Качество рекомендаций
Создание модели рекомендаций обычно является достаточно tooallow hello системные tooprovide рекомендации. Тем не менее качество рекомендаций варьируется в зависимости от использования hello обработки и hello покрытия hello каталога. Например, если у вас есть много новых элементов (элементов без значительных использования), система hello будет иметь трудностей предоставление рекомендаций для такого элемента или с помощью такого элемента как рекомендуемые. В порядке tooovercome hello холодного элемента проблему hello системы позволяет использовать hello метаданных hello элементы tooenhance hello рекомендаций. Эти метаданные являются tooas соответствующей функции. Примерами характеристик могут служить имена автора книги или актера фильма. Функции предоставляются через каталог hello в виде hello ключ значение. Hello полный формат файла каталога hello, можно найти toohello [импорта раздел каталога](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Сборка рейтинга
Возможности могут улучшить модель рекомендаций hello, однако toodo требуются hello использование значимых функций. В этих целях была введена новая сборка — сборка рейтинга. Эта сборка будет ранжирования полезность функции hello. Значимая характеристика имеет рейтинг не ниже 2.
Поняв, какие из функций hello важны, запустите сборку рекомендация список hello (или подсписок) значимых функций. Это возможно toouse, эти функции для расширения hello горячего элементов и новых элементов. В порядке toouse их для горячего элементов hello `UseFeatureInModel` параметр сборки должны быть настроены. В функции toouse заказа для новых элементов, hello `AllowColdItemPlacement` параметр сборки должен быть включен.
Примечание: Это не возможные tooenable `AllowColdItemPlacement` без включения `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Обоснование рекомендаций
Обоснование рекомендаций — еще один аспект использования характеристик. На самом деле engine hello Azure Machine Learning рекомендации можно использовать функции tooprovide рекомендация объяснения (так называемый рассуждения) начальные toomore достоверности в hello рекомендуется элемента от потребителя рекомендация hello.
tooenable рассуждения, hello `AllowFeatureCorrelation` и `ReasoningFeatureList` параметры должны быть toorequesting предыдущей установки сборки рекомендации.

## <a name="5-model-basic"></a>5. Базовая обработка модели
### <a name="51-create-model"></a>5.1. Создание модели
Создает запрос на создание модели.

| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelName |Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).<br>Максимальная длина: 20 |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

* `feed/entry/content/properties/id`— Содержит идентификатор hello модели.
  **Примечание**. В идентификаторе модели учитывается регистр.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="52-get-model"></a>5.2. Получение модели
Создает запрос на получение модели.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| id |Уникальный идентификатор hello модели (с учетом регистра) |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello модели данных можно найти в hello следующие элементы:

* `feed/entry/content/properties/Id` — уникальный идентификатор модели.
* `feed/entry/content/properties/Name` — имя модели.
* `feed/entry/content/properties/Date` — дата создания модели.
* `feed/entry/content/properties/Status` — состояние модели. Одно из следующих hello:
  * Created — модель создана и не содержит каталога и данных по использованию;
  * ReadyForBuild — модель создана и содержит каталог и данные по использованию.
* `feed/entry/content/properties/HasActiveBuild`— Указывает, если модель hello успешно создан.
* `feed/entry/content/properties/BuildId` — идентификатор активной сборки модели.
* `feed/entry/content/properties/Mpr` — средний процентильный рейтинг модели (MPR, подробнее см. в разделе, посвященном параметру ModelInsight).
* `feed/entry/content/properties/UserName` — имя внутреннего пользователя модели.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Получение всех моделей
Извлекает все модели hello текущего пользователя.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

* `feed/entry/content/properties/Id` — уникальный идентификатор модели.
* `feed/entry/content/properties/Name` — имя модели.
* `feed/entry/content/properties/Date` — дата создания модели.
* `feed/entry/content/properties/Status` — состояние модели. Одно из следующих hello:
  * Created — модель создана и не содержит каталога и данных по использованию;
  * ReadyForBuild — модель создана и содержит каталог и данные по использованию.
* `feed/entry/content/properties/HasActiveBuild`— Указывает, если модель hello успешно создан.
* `feed/entry/content/properties/BuildId` — идентификатор активной сборки модели.
* `feed/entry/content/properties/Mpr` — средний процентильный рейтинг модели (подробнее см. в разделе, посвященном параметру ModelInsight).
* `feed/entry/content/properties/UserName` — имя внутреннего пользователя модели.
* `feed/entry/content/properties/UsageFileNames` — список файлов использования модели через запятую.
* `feed/entry/content/properties/CatalogId` — идентификатор каталога модели.
* `feed/entry/content/properties/Description` — описание модели.
* `feed/entry/content/properties/CatalogFileName` — имя файла каталога модели.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Обновление модели
Вы можете обновить описание модели hello или hello идентификатором активного построения.<br>
<ins>Активный идентификатор сборки</ins> — каждая сборка каждой модели имеет собственный идентификатор. Идентификатор построения active Hello является первой успешной сборки hello всех новых моделей. После иметь идентификатор активного построения и выполнить дополнительные сборки для hello одной модели необходимо tooexplicitly задать его значение как hello по умолчанию идентификатор сборки, если требуется. После получения рекомендаций, если не указан идентификатор сборки hello нужного toouse, по умолчанию hello один будет использоваться автоматически.<br>
Этот механизм позволяет - после модели рекомендаций в производственной среде - toobuild новых моделей и проверить их, прежде чем продвинуть их tooproduction.

| Метод HTTP | URI |
|:--- |:--- |
| ОТПРАВКА |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| id |Уникальный идентификатор hello модели (с учетом регистра) |
| версия_API |1.0 |
|  | |
| Текст запроса |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Обратите внимание, что hello XML теги описание ActiveBuildId являются необязательными. Если вы не хотите tooset описание или ActiveBuildId, удалите весь тег hello. |

**Ответ**:

Код состояния HTTP: 200

### <a name="55----delete-model"></a>5.5.    Удаление модели
Удаляет существующую модель по идентификатору.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| id |Уникальный идентификатор hello модели (с учетом регистра) |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Расширенная обработка модели
### <a name="61----model-data-insight"></a>6.1.    Подробные сведения о данных модели
Возвращает статистические данные о данных об использовании hello, эта модель создавалась с.

Доступно только для сборки рекомендаций.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello данные возвращаются в виде коллекции свойств.

* `feed/entry/id/content/properties/key`-Содержит имя свойства hello.
* `feed/entry/id/content/properties/value`-Содержит значение свойства hello.

в следующей таблице Hello описывается hello значение, представляющее каждого ключа.

| Ключ | Описание |
|:--- |:--- |
| AvgItemLength |Среднее число отдельных пользователей на элемент. |
| AvgUserLength |Среднее число отдельных элементов на пользователя. |
| DensificationNumberOfItems |Количество элементов после удаления элементов, которые нельзя смоделировать. |
| DensificationNumberOfUsers |Количество точек использования после удаления пользователей и элементов, которые нельзя смоделировать. |
| DensificationNumberOfRecords |Количество точек использования после удаления пользователей и элементов, которые нельзя смоделировать. |
| MaxItemLength |Количество уникальных пользователей для наиболее популярных элемента hello. |
| MaxUserLength |Максимальное число отдельных элементов для пользователя. |
| MinItemLength |Максимальное число отдельных пользователей для элемента. |
| MinUserLength |Минимальное число отдельных элементов для пользователя. |
| RawNumberOfItems |Число элементов в файлах использования hello. |
| RawNumberOfUsers |Количество точек использования перед любыми операциями удаления. |
| RawNumberOfRecords |Количество точек использования перед любыми операциями удаления. |
| SamplingNumberOfItems |Недоступно |
| SamplingNumberOfRecords |Недоступно |
| SamplingNumberOfUsers |Недоступно |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Подробные сведения о модели
Возвращает модель, представление в hello active сборки или (если есть) на конкретную сборку.

Доступно только для сборки рекомендаций.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |С активным идентификатором сборки:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>С конкретным идентификатором сборки:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| buildId |Необязательно — число, которое обозначает успешную сборку. |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello данные возвращаются в виде коллекции свойств.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

в следующей таблице Hello описывается hello значение, представляющее каждого ключа.

| Ключ | Описание |
|:--- |:--- |
| CatalogCoverage |Какая часть hello каталога можно конфигураторе с шаблонами использования. остальные элементы hello Hello потребуется функции на основе содержимого. |
| Mpr |Ранжирование среднее процентиля hello модели. Чем меньше это значение, тем лучше. |
| NumberOfDimensions |Число измерений, используемых алгоритмом разложение hello матрицы. |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Получение образца модели
Получает образец hello модели рекомендаций.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>С конкретным идентификатором сборки:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

OData XML

Ответ возвращается в формате необработанного текста.

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Бизнес-правила модели
Эти типы hello поддерживается правил являются:

* <strong>Блокировки</strong> -блокировки позволяет tooprovide список элементы, которые не должны tooreturn в результатах рекомендация hello. 
* <strong>FeatureBlockList</strong> -функция блокировки позволяет вам tooblock элементов на основе значения hello его компонентов.

*Не добавляйте в один список блокировок больше 1000 позиций, иначе время ожидания вызова будет превышено. Если вам требуется tooblock более 1000 элементов, можно сделать несколько вызовов блокировки.*

* <strong>Upsale</strong> -Upsale позволяет tooenforce tooreturn элементы в результатах рекомендация hello.
* <strong>Белый список</strong> -белый список включает tooonly можно предложить рекомендаций из списка элементов.
* <strong>FeatureWhiteList</strong> -белый список функций включает tooonly рекомендуется элементы, имеющие значения определенного компонента.
* <strong>PerSeedBlockList</strong> — в список блокировок начальное значение включает tooprovide каждого элемента в список элементов, которые не возвращены в качестве рекомендаций.

### <a name="71----get-model-rules"></a>7.1.    Получение правил для модели
| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Пример:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

* `feed/entry/content/properties/Id` — уникальный идентификатор правила.
* `feed/entry/content/properties/Type`-Тип правила hello.
* `feed/entry/content/properties/Parameter` — параметр правила.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Добавление правила
| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| ЗАГОЛОВОК |`"Content-Type", "text/xml"` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| версия_API |1.0 |
|  | |
| Текст запроса | |

<ins>Всякий раз предоставления идентификаторы элементов для бизнес-правил, убедитесь, что toouse hello внешний идентификатор элемента hello (hello таким же идентификатором, который использовался в файл каталога hello)</ins><br>
<ins>tooadd правило блокировки:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureBlockList правила:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>tooadd правило Upsale:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd правила белого списка:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd FeatureWhiteList правила:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>tooadd PerSeedBlockList правила:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Ответ**:

Код состояния HTTP: 200

Hello API возвращает hello вновь созданные правила с сведения о нем. Свойство правила Hello можно получить из hello, следующие пути:

* `feed/entry/content/properties/Id` — уникальный идентификатор правила.
* `feed/entry/content/properties/Type`-Тип правила hello: блокировки или Upsale.
* `feed/entry/content/properties/Parameter` — параметр правила.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Удаление правила
| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| filterId |Уникальный идентификатор фильтра hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

### <a name="74----delete-all-rules"></a>7.4.    Удаление всех правил
| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

## <a name="8-catalog"></a>8. Каталог
### <a name="81----import-catalog-data"></a>8.1.    Импорт данных каталога
При передаче нескольких каталогов файлы toohello же модель с несколькими вызовами, будет вставлен только hello новые элементы каталога. Существующие элементы останутся на основе исходных значений hello. С помощью этого метода нельзя обновлять данные каталога.

данные каталога Hello следовать hello следующий формат:

* Без характеристик: `<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* С характеристиками: `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Примечание: hello максимальный размер файла — 200 МБ.

** Сведения о формате **

| Имя | Обязательно | Тип | Описание |
|:--- |:--- |:--- |:--- |
| Идентификатор элемента |Да |[A–z], [a–z], [0–9], [_] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;<br> Максимальная длина: 50 |Уникальный идентификатор элемента. |
| Имя элемента |Да |Любые алфавитно-цифровые символы<br> Максимальная длина: 255 |Имя элемента. |
| Категория элемента |Да |Любые алфавитно-цифровые символы <br> Максимальная длина: 255 |Категория toowhich этот элемент принадлежит (например кулинарии книг, Драма...); может быть пустым. |
| Описание |Нет, если только нет характеристик (но может быть пустым) |Любые алфавитно-цифровые символы <br> Максимальная длина: 4000 |Описание элемента. |
| Список характеристик |Нет |Любые алфавитно-цифровые символы <br> Максимальная длина: 4000; максимальное число компонентов: 20 |Список разделенных запятыми имя функции = функция значение, которое может быть рекомендация модели используется tooenhance; в разделе [дополнительные разделы](#2-advanced-topics) раздела. |

| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| ЗАГОЛОВОК |`"Content-Type", "text/xml"` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| filename |Текстовому идентификатору hello каталога.<br>Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).<br>Максимальная длина: 50 |
| версия_API |1.0 |
|  | |
| Текст запроса |Пример (с компонентами):<br/>2406e770-769c-4189-89de-1c9283f93a96, Callan Клара, книгу, название книги hello, создавать = Wright Ричард publisher = Harper Flamingo Канада, год = 2001 г.<br>hello 21bf8088-b6c0-4509-870c-e1c7ac78304a, Forgetting комнате: фантастики (Byzantium книга), книга, создавать = Bantock ник publisher = Harpercollins, год = 1997<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, солидарности ответ, книгу, название книги hello, создавать = фабрики Magnus издателя публикации галереей = год = 1998</pre> |

**Ответ**:

Код состояния HTTP: 200

Hello API возвращает отчет hello импорта.

* `feed\entry\content\properties\LineCount` — количество принятых строк.
* `feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Получение каталога
Извлекает все элементы каталога.
Hello каталога будут получены одной странице одновременно. Для поиска элементов tooget с определенного индекса, можно использовать параметр hello $skip odata. Для экземпляра tooget элементов, начиная с позиции 100 следует добавить параметр hello $skip = 100 toohello запрос.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого элемента каталога. Каждая запись имеет hello следующие данные:

* `feed/entry/content/properties/ExternalId`-Каталога внешний идентификатор элемента, одно — предоставляемое клиента hello hello.
* `feed/entry/content/properties/InternalId`-Каталога внутренний идентификатор элемента, hello, создавший Azure Machine Learning рекомендации.
* `feed/entry/content/properties/Name` — имя элемента каталога.
* `feed/entry/content/properties/Category` — категория элемента каталога.
* `feed/entry/content/properties/Description` — описание элемента каталога.
* `feed/entry/content/properties/Metadata` — метаданные элемента каталога.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Получение элементов каталога по токену
| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| token |Имя элемента каталога hello маркер. Должен содержать не менее трех символов. |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого элемента каталога. Каждая запись имеет hello следующие данные:

* `feed/entry/content/properties/InternalId`-Каталога внутренний идентификатор элемента, hello, создавший Azure Machine Learning рекомендации.
* `feed/entry/content/properties/Name` — имя элемента каталога.
* `feed/entry/content/properties/Rating` — (для будущего использования).
* `feed/entry/content/properties/Reasoning` — (для будущего использования).
* `feed/entry/content/properties/Metadata` — (для будущего использования).
* `feed/entry/content/properties/FormattedRating` — (для будущего использования).

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Данные об использовании
### <a name="91----import-usage-data"></a>9.1.    Импорт данных по использованию
#### <a name="911-uploading-file"></a>9.1.1. Передача файла
В этом разделе показано, как данные об использовании tooupload с помощью файла. Можно вызывать этот API несколько раз с данными об использовании. Для всех вызовов сохранятся все данные об использовании.

| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| filename |Текстовому идентификатору hello каталога.<br>Допускаются только буквы (A–Z, a–z), цифры (0–9), дефисы (-) и символы подчеркивания (_).<br>Максимальная длина: 50 |
| версия_API |1.0 |
|  | |
| Текст запроса |Данные об использовании. Формат:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Имя</th><th>Обязательно</th><th>Тип</th><th>Описание</th></tr><tr><td>Идентификатор пользователя</td><td>Да</td><td>[A–z], [a–z], [0–9], [_] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;<br> Максимальная длина: 255 </td><td>Уникальный идентификатор пользователя</td></tr><tr><td>Идентификатор элемента</td><td>Да</td><td>[A-z], [a-z], [0-9], [&#95;] &#40;символ подчеркивания&#41;, [-] &#40;дефис&#41;<br> Максимальная длина: 50</td><td>Уникальный идентификатор элемента.</td></tr><tr><td>Время</td><td>Нет</td><td>Дата в формате: ГГГГ/ММ/ДДТЧЧ:ММ:СС (например, 2013/06/20Т10:00:00)</td><td>Время данных</td></tr><tr><td>Событие</td><td>Нет. Если указано, необходимо также указать дату</td><td>Одно из следующих hello:<br>• Click<br>• RecommendationClick<br>• AddShopCart<br>• RemoveShopCart<br>• Покупка</td><td></td></tr></table><br>Максимальный размер файла: 200 МБ.<br><br>Пример:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Ответ**:

Код состояния HTTP: 200

* `Feed\entry\content\properties\LineCount` — количество принятых строк.
* `Feed\entry\content\properties\ErrorCount`-Число строк, которые не были вставлены из-за ошибки tooan.
* `Feed\entry\content\properties\FileId` — идентификатор файла.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Использование функции сбора данных
В этом разделе показано, как toosend событий в реальном времени tooAzure машины обучения рекомендации, обычно с веб-сайта.

| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| ЗАГОЛОВОК |`"Content-Type", "text/xml"` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| версия_API |1.0 |
| Тело запроса |Записи данных событий для каждого события необходимо toosend. Для hello одного сеанса пользователя или браузера hello таким же Идентификатором hello SessionId поля, необходимо отправить. (Пример текста события см. ниже.) |

* Пример события Click:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Пример события RecommendationClick:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Пример события AddShopCart:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Пример события RemoveShopCart:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
              <EventData>
                      <Name>RemoveShopCart</Name>
                      <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                </EventData>
          </EventData>
        </Event>
* Пример события Purchase:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* Пример отправки событий двух типов, Click и AddShopCart:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Ответ**. Код состояния HTTP: 200

### <a name="92----list-model-usage-files"></a>9.2.    Вывод списка файлов использования модели
Извлекает метаданные из всех файлов использования модели.
Hello об использовании файлы будут получены одной странице одновременно. Каждая страница содержит 100 элементов. Для поиска элементов tooget с определенного индекса, можно использовать параметр hello $skip odata. Для экземпляра tooget элементов, начиная с позиции 100 следует добавить параметр hello $skip = 100 toohello запрос.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| forModelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello ответ содержит одну запись для использования файла. Каждая запись имеет hello следующие данные:

* `feed\entry\content\properties\Id` — идентификатор файла использования.
* `feed\entry\content\properties\Length` — размер файла использования в мегабайтах.
* `feed\entry\content\properties\DateModified`-Дата создания файла использования hello.
* `feed\entry\content\properties\UseInModel`-Файл для использования hello использование в модели hello.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Получение статистики использования
Получает статистику использования.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| startDate |Дата начала. Формат: гггг/ММ/ддТЧЧ:мм:сс |
| endDate |Дата окончания. Формат: гггг/ММ/ддТЧЧ:мм:сс |
| eventTypes |Строки с разделителями запятыми события типы или null tooget все события |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Коллекция элементов "ключ-значение". Каждый из них содержит сумму hello событий для определенного типа событий группируются по часам.

* `feed\entry[i]\content\properties\Key`— Содержит время hello (сгруппированный по часам) и типа события hello.
* `feed\entry[i]\content\properties\Value` — общее число событий.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Получение образца файла использования
Извлекает hello первый 2 КБ, использование содержимого файла.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| fileId |Уникальный идентификатор hello модель использования файла |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Ответ возвращается в формате необработанного текста.

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Получение файла использования модели
Извлекает полное содержимое hello hello использования файла.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| mid |Уникальный идентификатор модели hello |
| fid |Уникальный идентификатор hello модель использования файла |
| загрузить |1 |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Ответ возвращается в формате необработанного текста.

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Удаление файла использования
Удаляет файл использования hello указанной модели.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| fileId |Уникальный идентификатор hello файл toobe удалена |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Удаление всех файлов использования
Удаляет все файлы использования модели.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

## <a name="10-features"></a>10. Функции
В этом разделе показано, как tooretrieve функции сведения, такие как функции hello импортирован и их значения, рангу, и при этом ранг был выделен. Функции, импортируются как часть данных каталога hello, а затем рангу связанного при завершения rank сборки.
Функция rank можно изменить соответствующим toohello модель данных об использовании и типа элементов. Но ранг hello согласованное использование/элементы должны быть только небольшие отклонения.
Ранг Hello функций является неотрицательным числом. Hello с номером 0 означает не присваивается ранг этой функции hello (происходит при вызове этого API завершения предыдущего toohello первого построения rank hello). Дата Hello, по которому отмеченное ранг hello называется актуальность оценка hello.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Получение информации о характеристиках (для последней сборки рейтинга)
Извлекает сведения о функции hello, включая ранжирования для последней hello успешной rank сборки.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| samplingSize |Количество tooinclude значения для каждого компонента, в соответствии с toohello данных, содержащихся в каталоге hello. <br/>Возможные значения:<br> -1 — все образцы; <br>0 — ни одного образца; <br>N — возвращается N образцов для каждого имени компонента. |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello ответ содержит список записей сведения о функции. Каждая запись содержит следующие сведения:

* `feed/entry/content/m:properties/d:Name` — название характеристики.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Дата в какой hello ранг функция выделенный toothis так называемый актуальность оценки. Историческая дата ("0001-01-01T00:00:00") означает, что сборка рейтинга еще не выполнялась.
* `feed/entry/content/m:properties/d:Rank` — рейтинг характеристики (число с плавающей запятой). При рейтинге не менее 2,0 характеристика считается значимой.
* `feed/entry/content/m:properties/d:SampleValues`-Запятыми список значений, размер выборки toohello на запросе.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Получение информации о характеристиках (для определенной сборки рейтинга)
Извлекает сведения о функции hello, включая релевантности для конкретного построения rank hello.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| samplingSize |Количество tooinclude значения для каждого компонента, в соответствии с toohello данных, содержащихся в каталоге hello.<br/> Возможные значения:<br> -1 — все образцы; <br>0 — ни одного образца; <br>N — возвращается N образцов для каждого имени компонента. |
| rankBuildId |Уникальный идентификатор сборки rank hello или -1 для последнего построения rank hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

Hello ответ содержит список записей сведения о функции. Каждая запись содержит следующие сведения:

* `feed/entry/content/m:properties/d:Name` — название характеристики.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Дата в какой hello ранг функция выделенный toothis так называемый актуальность оценки. Историческая дата ("0001-01-01T00:00:00") означает, что сборка рейтинга еще не выполнялась.
* `feed/entry/content/m:properties/d:Rank` — рейтинг характеристики (число с плавающей запятой). При рейтинге не менее 2,0 характеристика считается значимой.
* `feed/entry/content/m:properties/d:SampleValues`-Запятыми список значений, размер выборки toohello на запросе.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Создание
  В этом разделе описывается hello различные интерфейсы API, связанные с toobuilds. Существует три типа сборок: сборка рекомендаций, сборка рейтингов и сборка FBT (часто покупаемая вместе с ними).

Назначение Hello рекомендация сборки — toogenerate модели рекомендаций, использовать для составления прогнозов. Прогнозы (для сборок этого типа) бывают двух типов:

* I2I — т. н. Элемент рекомендации tooItem - заданный элемент или список элементов, этот параметр будет прогнозироваться список элементов, которые, скорее всего, toobe высокий интерес.
* U2I — т. н. Рекомендации tooItem пользователя - заданы идентификатор пользователя (а при необходимости список элементов) этот параметр будет прогнозироваться список элементов, которые, скорее всего, toobe высокий интерес для hello заданным пользователем (и его выбора дополнительных элементов). Hello U2I рекомендации основываются на историю hello элементы, представляющие интерес для пользователя hello toohello время построения модели hello.

Rank построение, которое технические, позволяющий toolearn о hello полезность ваши возможности. Как правило в порядке tooget hello добиться наилучших результатов для модели рекомендаций, включающие функции, должен выполнить hello следующие шаги:

* Активация rank сборки (если оценка hello ваши возможности стабильна) и подождите, пока вы получаете оценка функции hello.
* Получить ваши возможности ранг hello, вызывающему Привет [получить сведения о функции](#101-get-features-info-for-last-rank-build) API.
* Настройте сборки рекомендация hello следующие параметры:
  * `useFeatureInModel`-Set tooTrue.
  * `ModelingFeatureList`-Set tooa запятыми список функций со скоростью не менее 2.0 (в соответствии с toohello рангов, полученный в предыдущем шаге hello).
  * `AllowColdItemPlacement`-Set tooTrue.
  * При необходимости можно задать `EnableFeatureCorrelation` tooTrue и `ReasoningFeatureList` toohello список компонентов, которые вы хотите toouse объяснение (обычно hello же список компонентов, используются для моделирования или подчиненный список).
* Активация сборки hello рекомендации с параметрами настройки hello.

Примечание: Если не задан, все параметры (например, вызов сборки рекомендация hello без параметров) или явно не отключайте hello использования функций (например `UseFeatureInModel` задать tooFalse), системы hello описывается настройка параметров, связанных с функции hello toohello описано выше значения, в случае, если существует rank сборки.

Не существует ограничения на выполнении rank построения и рекомендации построить одновременно для hello же модели. Тем не менее не может запустить две сборки hello того же типа на hello же модели в параллельном режиме.

Сборка FBT (Frequently Bought Together, "С этим товаром часто покупают") — это еще один алгоритм рекомендаций, иногда называемый консервативным. Он подходит для каталогов, которые по своему характеру являются неоднородными (однородные каталоги: книги, фильмы, продукты питания, одежда; неоднородные: компьютеры и устройства, товары из разных областей, большое многообразие).

Примечание: Если hello использования файлы, загруженные содержат hello необязательное поле «Тип событий» нажмите для взноса по моделирования только события «Покупки» будет использоваться. Если тип события не указан, все события будут рассматриваться как покупки.

#### <a name="111-build-parameters"></a>11.1. Параметры сборки
Каждый тип сборки можно настроить с помощью набора параметров (описанных ниже). Если не настроить параметры hello, hello системы будет автоматически атрибута toohello сведения присутствуют во время hello запустить сборку в соответствии с параметрами toohello значения.

##### <a name="1111-usage-condenser"></a>11.1.1. Уплотнение данных по использованию
Пользователи и элементы с небольшим числом точек использования могут создавать больше шума, чем информации. Hello система пытается toopredict hello минимальное число точек использования каждого toobe пользователя или элемента, используемого в модели. Это число будет находиться в пределах диапазона hello, определенных hello ItemCutoffLowerBound и параметрах ItemCutoffUpperBound для hello диапазона, определенные hello UserCutOffLowerBound и UserCutoffUpperBound параметров для пользователей и элементов. Hello конденсатор влияет на элементы или пользователей можно минимизировать путем настройки по крайней мере один из соответствующих границ toozero hello.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Параметры сборки рейтингов
в следующей таблице Hello описывается hello параметров построения для ранжирования сборки.

| Ключ | Описание | Тип | Допустимое значение |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели. большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени. |Целое число  |10–50 |
| NumberOfModelDimensions |Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных. Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры. Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами. |Целое число  |10-40 |
| ItemCutOffLowerBound |Определяет нижнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| ItemCutOffUpperBound |Определяет верхнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffLowerBound |Определяет hello пользователя нижнюю границу конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffUpperBound |Определяет верхнюю границу пользователя hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Параметры сборки рекомендаций
в следующей таблице Hello описывается hello параметров построения для построения рекомендации.

| Ключ | Описание | Тип | Допустимое значение |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели. большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени. |Целое число  |10–50 |
| NumberOfModelDimensions |Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных. Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры. Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами. |Целое число  |10-40 |
| ItemCutOffLowerBound |Определяет нижнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| ItemCutOffUpperBound |Определяет верхнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffLowerBound |Определяет hello пользователя нижнюю границу конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffUpperBound |Определяет верхнюю границу пользователя hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| Описание |Описание сборки. |Строка |Любой текст, максимум 512 символов. |
| EnableModelingInsights |Позволяет toocompute метрики в модели рекомендаций hello. |Логический |True или False |
| UseFeaturesInModel |Указывает, если функции могут использоваться в модели рекомендаций hello tooenhance заказа. |Логический |True или False |
| ModelingFeatureList |Список разделенных запятыми toobe имена компонентов, используемых в построении hello рекомендация, в порядке tooenhance hello рекомендации. |Строка |Имена компонентов, копирование too512 символов |
| AllowColdItemPlacement |Указывает, если рекомендация hello также будет принудительно новых элементов через компонент подобия. |Логический |True или False |
| EnableFeatureCorrelation |Указывает, можно ли использовать характеристику в обосновании. |Логический |True или False |
| ReasoningFeatureList |Список разделенных запятыми toobe имена компонентов для рассуждения предложения (например описания рекомендации). |Строка |Имена компонентов, копирование too512 символов |
| EnableU2I |Разрешить так называемый hello персонализированных рекомендаций U2I (рекомендациями tooitem пользователя). |Логический |True или False (по умолчанию True) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. Параметры сборки FBT
в следующей таблице Hello описывается hello параметров построения для построения рекомендации.

| Ключ | Описание | Тип | Допустимое значение (по умолчанию) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Как модель консервативной hello. Количество вхождений совместно для моделирования toobe элементов. |Целое число  |3–50 (6) |
| FbtMaxItemSetSize |Количество элементов в наборе часто Здравствуйте, границ. |Целое число  |2–3 (2) |
| FbtMinimalScore |Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результаты. Hello выше hello лучше. |Double |0 и выше (0) |
| FbtSimilarityFunction |Определяет toobe функция подобия hello, используемые сборки hello. Serendipity, повышает вероятность точности прогнозов и сопутствующих вхождения повышает вероятность предсказуемость Жаккарда является хорошо компромисс между двумя hello. |Строка |cooccurrence, точность, jaccard (точность) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Запуск сборки рекомендаций
  По умолчанию этот интерфейс API запускает сборку модели рекомендаций. tootrigger ранг сборки (в порядке tooscore функции), следует использовать вариант API hello сборки с параметром типа сборки.

| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| ЗАГОЛОВОК |`"Content-Type", "text/xml"` (при отправке текста запроса) |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userDescription |Текстовому идентификатору hello каталога. Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См. пример выше.<br>Максимальная длина: 50 |
| версия_API |1.0 |
|  | |
| Текст запроса |Если оставить пустым hello построения будет выполняться с параметры сборки по умолчанию hello.<br><br>Параметры сборки hello tooset следует отправьте параметры hello в XML-ФАЙЛЕ в текст hello как следующий образец hello. (См. раздел hello «параметры построения» объяснение параметров hello).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Ответ**:

Код состояния HTTP: 200

Это асинхронный интерфейс API. В качестве ответа вы получите идентификатор сборки. tooknow после окончания сборки hello, следует вызвать API hello «Получить строит состояние из модели» и найдите этот идентификатор построения в ответ hello. Обратите внимание, что сборка может занять от toohours минут в зависимости от размера данных hello hello.

Пока hello сборки завершается, не должны занимать рекомендации.

Допустимые состояния сборки:

* Create — запрос сборки был создан;
* Queued — запрос сборки был отправлен и поставлен в очередь;
* Building — выполняется сборка;
* Success — сборка успешно завершилась;
* Error — сборка завершилась сбоем;
* Cancelled — сборка отменена;
* Отмена - был отправлен запрос на отмену для построения hello.

Обратите внимание, hello пути не удается найти идентификатор сборки hello.`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Запуск сборки (рекомендаций, рейтингов или FBT)
| Метод HTTP | URI |
|:--- |:--- |
| ПУБЛИКАЦИЯ |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| ЗАГОЛОВОК |`"Content-Type", "text/xml"` (при отправке текста запроса) |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userDescription |Текстовому идентификатору hello каталога. Обратите внимание: при использовании пробелов их необходимо заменить сочетанием символов %20 См. пример выше.<br>Максимальная длина: 50 |
| buildType |Тип tooinvoke hello сборки: <br/> – Recommendation — для сборки рекомендаций. <br> – Ranking — для сборки рейтинга. <br/> – Fbt — для сборки FBT. |
| версия_API |1.0 |
|  | |
| Текст запроса |Если оставить пустым hello построения будет выполняться с параметры сборки по умолчанию hello.<br><br>Параметры сборки tooset, отправьте их в XML-ФАЙЛЕ в текст hello, как и в следующий образец hello. (См. раздел hello «параметры построения» содержатся пояснения и полный список параметров hello).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Ответ**:

Код состояния HTTP: 200

Это асинхронный интерфейс API. В качестве ответа вы получите идентификатор сборки. tooknow после окончания сборки hello, следует вызвать API hello «Получить строит состояние из модели» и найдите этот идентификатор построения в ответ hello. Обратите внимание, что сборка может занять от toohours минут в зависимости от размера данных hello hello.

Пока hello сборки завершается, не должны занимать рекомендации.

Допустимые состояния сборки:

* Create — модель создана;
* Queued — сборка модели запущена и поставлена в очередь;
* Building — сборка модели выполняется;
* Success — сборка успешно завершилась;
* Error — сборка завершилась сбоем;
* Cancelled — сборка отменена;
* Cancelling — сборка отменяется.

Обратите внимание, hello пути не удается найти идентификатор сборки hello.`Feed\entry\content\properties\Id`

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>




### <a name="114-get-builds-status-of-a-model"></a>11.4. Получение статусов сборок модели
Извлекает сборки определенной модели с указанием их состояния.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| onlyLastBuild |Указывает ли все hello tooreturn строить журнал hello модели или только hello состояние последнего построения hello |
| версия_API |1.0 |

**Ответ**:

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого построения. Каждая запись имеет hello следующие данные:

* `feed/entry/content/properties/UserName`— Имя пользователя hello.
* `feed/entry/content/properties/ModelName`-Имя модели hello.
* `feed/entry/content/properties/ModelId` — уникальный идентификатор модели.
* `feed/entry/content/properties/IsDeployed`-Сборки hello развернут ли (так) активная сборка).
* `feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.
* `feed/entry/content/properties/BuildType`-Тип сборки hello.
* `feed/entry/content/properties/Status` — состояние сборки. Может принимать одно из следующих hello: ошибка, построение, в очереди, отменяется, отменено, успех.
* `feed/entry/content/properties/StatusMessage`-Сообщение сведения о состоянии (применяется только toospecific состояния).
* `feed/entry/content/properties/Progress` — ход выполнения сборки (%).
* `feed/entry/content/properties/StartTime` — время начала сборки.
* `feed/entry/content/properties/EndTime` — время окончания сборки.
* `feed/entry/content/properties/ExecutionTime` — длительность сборки.
* `feed/entry/content/properties/ProgressStep`— Сведения о текущей стадии hello построения выполняется.

Допустимые состояния сборки:

* Created — запись запроса сборки создана;
* Queued — запрос сборки инициирован и помещен в очередь;
* Building — сборка выполняется;
* Success — сборка успешно завершилась;
* Error — сборка завершилась сбоем;
* Cancelled — сборка отменена;
* Cancelling — сборка отменяется.

Допустимые значения типа сборки:

* Rank — сборка рейтинга;
* Recommendation — сборка рекомендаций.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="115-get-builds-status"></a>11.5. Получение состояний сборок
Извлекает состояния сборок всех моделей пользователя.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| onlyLastBuild |Указывает ли все hello tooreturn строить журнал hello модели или только состояние hello hello последнюю сборку. |
| версия_API |1.0 |

**Ответ**:

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого построения. Каждая запись имеет hello следующие данные:

* `feed/entry/content/properties/UserName`— Имя пользователя hello.
* `feed/entry/content/properties/ModelName`-Имя модели hello.
* `feed/entry/content/properties/ModelId` — уникальный идентификатор модели.
* `feed/entry/content/properties/IsDeployed`-Ли hello сборка развертывается.
* `feed/entry/content/properties/BuildId` — уникальный идентификатор сборки.
* `feed/entry/content/properties/BuildType`-Тип сборки hello.
* `feed/entry/content/properties/Status` — состояние сборки. Может принимать одно из следующих hello: ошибка, построение, в очереди, отменено, отменяется, успех.
* `feed/entry/content/properties/StatusMessage`-Сообщение сведения о состоянии (применяется только toospecific состояния).
* `feed/entry/content/properties/Progress` — ход выполнения сборки (%).
* `feed/entry/content/properties/StartTime` — время начала сборки.
* `feed/entry/content/properties/EndTime` — время окончания сборки.
* `feed/entry/content/properties/ExecutionTime` — длительность сборки.
* `feed/entry/content/properties/ProgressStep`— Сведения о текущей стадии hello построения выполняется.

Допустимые состояния сборки:

* Created — запись запроса сборки создана;
* Queued — запрос сборки инициирован и помещен в очередь;
* Building — сборка выполняется;
* Success — сборка успешно завершилась;
* Error — сборка завершилась сбоем;
* Cancelled — сборка отменена;
* Cancelling — сборка отменяется.

Допустимые значения типа сборки:

* Rank — сборка рейтинга;
* Recommendation — сборка рекомендаций.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="116-delete-build"></a>11.6. Удаление сборки
Удаление сборки

Примечание. <br>Активные сборки не удаляются. Hello модели должен быть обновлен tooa другого активного построения перед его удалением.<br>Выполняющуюся сборку нельзя удалить. Сначала отмените hello сборки путем вызова <strong>отменить построение</strong>.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| buildId |Уникальный идентификатор сборки hello. |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

### <a name="117-cancel-build"></a>11.7. Отмена сборки
Отменяет выполняющуюся сборку.

| Метод HTTP | URI |
|:--- |:--- |
| ОТПРАВКА |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| buildId |Уникальный идентификатор сборки hello. |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

### <a name="118-get-build-parameters"></a>11.8. Получение параметров сборки
Извлекает параметры сборки.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| buildId |Уникальный идентификатор сборки hello. |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Этот интерфейс API возвращает коллекцию элементов "ключ-значение". Каждый элемент представляет параметр и его значение:

* `feed/entry/content/properties/Key` — имя параметра сборки.
* `feed/entry/content/properties/Value` — значение параметра сборки.

в следующей таблице Hello описывается hello значение, представляющее каждого ключа.

| Ключ | Описание | Тип | Допустимое значение |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |hello отражается Hello числа итераций, выполняет hello модели в целом вычислений времени и hello точности модели. большее число hello Hello, hello повышает точность, вы получите, но hello вычислений времени займет больше времени. |Целое число  |10–50 |
| NumberOfModelDimensions |Hello число измерений относится toohello число hello модели «компоненты» будет повторить toofind в данных. Увеличение числа hello измерений позволит лучше выполнять тонкую настройку hello результаты на более мелкие кластеры. Однако слишком большое число измерений сделает невозможным модели hello поиск корреляции между элементами. |Целое число  |10-40 |
| ItemCutOffLowerBound |Определяет нижнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| ItemCutOffUpperBound |Определяет верхнюю границу элемента hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffLowerBound |Определяет hello пользователя нижнюю границу конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| UserCutOffUpperBound |Определяет верхнюю границу пользователя hello конденсатор hello. См. раздел, посвященный уплотнению данных по использованию, выше. |Число |2 или более (0 — отключить уплотнение) |
| Описание |Описание сборки. |Строка |Любой текст, максимум 512 символов. |
| EnableModelingInsights |Позволяет toocompute метрики в модели рекомендаций hello. |Логический |True или False |
| UseFeaturesInModel |Указывает, если функции могут использоваться в модели рекомендаций hello tooenhance заказа. |Логический |True или False |
| ModelingFeatureList |Список разделенных запятыми toobe имена компонентов, используемых в построении hello рекомендация, в порядке tooenhance hello рекомендации. |Строка |Имена компонентов, копирование too512 символов |
| AllowColdItemPlacement |Указывает, если рекомендация hello также будет принудительно новых элементов через компонент подобия. |Логический |True или False |
| EnableFeatureCorrelation |Указывает, можно ли использовать характеристику в обосновании. |Логический |True или False |
| ReasoningFeatureList |Список разделенных запятыми toobe имена компонентов для рассуждения предложения (например описания рекомендации). |Строка |Имена компонентов, копирование too512 символов |

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Рекомендации
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Получение рекомендаций по элементам (для активной сборки)
Узнать hello active построения типа «Рекомендации» или «Взноса по» на основе списка элементов начальные значения (input).

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| itemIds |Список разделенных запятыми hello toorecommend элементы для. <br>Если активный сборки hello имеет тип взноса по, затем можно передать только один элемент. <br>Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. <br> Макс. 150 |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа Hello ниже включает 10 рекомендуемые элементы.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Получение рекомендаций по элементам (для определенной сборки)
Получение рекомендаций определенной сборки типа Recommendation или Fbt.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| itemIds |Список разделенных запятыми hello toorecommend элементы для. <br>Если активный сборки hello имеет тип взноса по, затем можно передать только один элемент. <br>Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. <br> Макс. 150 |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| buildId |Hello построения toouse идентификатор для этого запроса рекомендаций |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.1.

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. Получение рекомендаций FBT (для активной сборки)
Получите рекомендации hello active построения типа взноса» по» на основе начального значения (input) элемента.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| itemId |Элемент toorecommend для. <br>Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. <br>Макс. 150 |
| minimalScore |Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результатов |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого набора рекомендуемых элементов (набор элементов, которые обычно купил вместе с элемента начального значения и входных hello). Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id1` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name1`-Имя элемента hello.
* `Feed\entry\content\properties\Id2` — идентификатор второго рекомендованного элемента (необязательно).
* `Feed\entry\content\properties\Name2`-Имя hello 2-й элемент (необязательно).
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа Hello ниже включает три набора рекомендуемых элементов.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Получение рекомендаций FBT (для определенной сборки)
Получение рекомендаций типа Fbt для определенной сборки.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| itemId |Элемент toorecommend для. <br>Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. <br>Макс. 150 |
| minimalScore |Минимальный показатель, который часто набор должен в порядке toobe, включенных в hello возвратили результатов |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| buildId |Hello построения toouse идентификатор для этого запроса рекомендаций |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого набора рекомендуемых элементов (набор элементов, которые обычно купил вместе с элемента начального значения и входных hello). Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id1` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name1`-Имя элемента hello.
* `Feed\entry\content\properties\Id2` — идентификатор второго рекомендованного элемента (необязательно).
* `Feed\entry\content\properties\Name2`-Имя hello 2-й элемент (необязательно).
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.3.

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Получение пользовательских рекомендаций (для активной сборки)
Получение пользовательских рекомендаций для сборки типа Recommendation, отмеченной как активная сборка.

Возвращает список прогнозируемый элемент, историю использования toohello hello пользователя в соответствии с Hello API.

Примечания: 

1. Для сборки FBT нет пользовательских рекомендаций.
2. Если построение hello active — взноса по, этот метод завершается с ошибкой.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userId |Уникальный идентификатор пользователя hello |
| numberOfResults |Требуемое число результатов. |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.1.

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Получение пользовательских рекомендаций со списком элементов (для активной сборки)
Получение пользовательских рекомендаций для сборки типа Recommendation, отмеченной как активная сборка, с дополнительным списком элементов.

Hello API вернет список прогнозируемый элемент, в соответствии с Хронология использования toohello пользователя hello и hello дополнительных указанных элементов.

Примечания: 

1. Для сборки FBT нет пользовательских рекомендаций.
2. Если построение hello active — взноса по, этот метод завершается с ошибкой.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userId |Уникальный идентификатор пользователя hello |
| itemsIds |Список разделенных запятыми hello toorecommend элементы для. Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.1.

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Получение пользовательских рекомендаций (для определенной сборки)
Получение пользовательских рекомендаций для определенной сборки типа Recommendation.

Возвращает список прогнозируемый элемент, историю использования toohello hello пользователя (используется в конкретной сборке hello) в соответствии с Hello API.

Примечание. Для сборки FBT нет пользовательских рекомендаций.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userId |Уникальный идентификатор пользователя hello |
| numberOfResults |Требуемое число результатов. |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| buildId |Hello построения toouse идентификатор для этого запроса рекомендаций |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.1.

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Получение пользовательских рекомендаций со списком элементов (для определенной сборки)
Получите рекомендации пользователя определенного построения типа «Рекомендации» и hello список дополнительных элементов.

Возвращает список прогнозируемого товара, журнал использования toohello пользователя hello и hello дополнительный список из элементов в соответствии с Hello API.

Примечание. Для сборки FBT нет пользовательских рекомендаций.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| userId |Уникальный идентификатор пользователя hello |
| itemIds |Список разделенных запятыми hello toorecommend элементы для. Максимальная длина: 1024 |
| numberOfResults |Требуемое число результатов. |
| includeMetatadata |Для использования в будущем, всегда имеет значение false |
| buildId |Hello построения toouse идентификатор для этого запроса рекомендаций |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating`-Оценка рекомендаций hello; выше число, тем выше уверенность в том.
* `Feed\entry\content\properties\Reasoning` — обоснование рекомендации (например, объяснения).

Пример ответа см. в подразделе 12.1.

## <a name="13-user-usage-history"></a>13. Журнал работы пользователей
После построения модели рекомендаций был hello система позволит tooretrieve hello журнал пользователей (элементов связанного tooa пользователя) используется для построения hello.
Этот API разрешить tooretrieve hello пользовательского журнала

Примечание: hello журнал пользователей сейчас доступен только для сборок рекомендации.

### <a name="131-retrieve-user-history"></a>13.1 Получения журнала пользователя
Получить список hello элемента используется в активных hello построения или в указанный hello сборки для hello указанный идентификатор пользователя.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |Просмотреть журнал hello пользователя для построения active hello.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Просмотреть журнал hello пользователей для заданного построения hello`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Пример:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор Hello hello модели. |
| userId |Hello уникальный идентификатор hello. |
| buildId |Необязательный параметр Разрешить tooindicate, из какой сборке hello журнал пользователей должно быть выборки |
| версия_API |1.0 |

**Ответ.**

Код состояния HTTP: 200

Hello ответ включает одной записи для каждого рекомендуемых элементов. Каждая запись имеет hello следующие данные:

* `Feed\entry\content\properties\Id` — идентификатор рекомендованного элемента.
* `Feed\entry\content\properties\Name`-Имя элемента hello.
* `Feed\entry\content\properties\Rating` — Недоступно.
* `Feed\entry\content\properties\Reasoning` — Недоступно.

OData XML

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Уведомления
Рекомендации обучения Azure машины создает уведомления при возникновении вызваны ошибками в системе hello. Существует 3 типа уведомлений:

1. Сбой сборки — срабатывает при каждом сбое сборки.
2. Получение данных, обрабатывающий сбой - это уведомление срабатывает, когда у нас есть более 100 ошибок в hello последние 5 минут в hello обработки событий использования в модели.
3. Сбой потребления рекомендации — это уведомление срабатывает, когда у нас есть более 100 ошибок в hello последние 5 минут в hello обработки запросов рекомендацию в модели.

### <a name="141-get-notifications"></a>14.1. Получение уведомлений
Получает все уведомления hello для всех моделей или для одной модели.

| Метод HTTP | URI |
|:--- |:--- |
| ПОЛУЧЕНИЕ |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Получение всех уведомлений для всех моделей:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Пример получения уведомлений для определенной модели:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Необязательный параметр. Если он не указан, вы получите все уведомления для всех моделей. <br>Допустимое значение: Уникальный идентификатор hello модели. |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ.**

Код состояния HTTP: 200

OData XML

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Удаление уведомлений модели
Удаляет все прочитанные уведомления для модели.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Пример:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| modelId |Уникальный идентификатор модели hello |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

### <a name="143-delete-user-notifications"></a>14.2. Удаление уведомлений пользователя
Удаляет все уведомления для всех моделей.

| Метод HTTP | URI |
|:--- |:--- |
| УДАЛИТЬ |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Имя параметра | Допустимые значения |
|:--- |:--- |
| версия_API |1.0 |
|  | |
| Текст запроса |НЕТ |

**Ответ**:

Код состояния HTTP: 200

## <a name="15-legal"></a>15. Юридическая информация
Данный документ предоставляется "как есть". Сведения и мнения, содержащиеся в этом документе, включая URL-адреса и другие ссылки на веб-сайты, могут быть изменены без предварительного уведомления.<br><br>
Некоторые примеры, содержащиеся в данном документе, являются вымышленными и приводятся исключительно в демонстрационных целях. Любое сходство с реальными ситуациями случайно.<br><br>
Этот документ не предоставляет никаких законных прав интеллектуальной собственности tooany в продуктах корпорации Майкрософт. Вы можете скопировать и использовать данный документ для внутренних справочных целей.<br><br>
© Корпорация Майкрософт (Microsoft Corporation), 2015 г. Все права защищены.

