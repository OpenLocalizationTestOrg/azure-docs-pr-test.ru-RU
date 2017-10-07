---
title: "aaaGuide toocreating службы данных для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развертывать службу данных для приобретения на hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Общее представление о схеме hello узлы для сопоставления существующих tooOData службы web, через CSDL
> [!IMPORTANT]
> **В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.** Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners). Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

В этом документе для пояснения hello узла структуры для сопоставления tooCSDL протокол OData. Очень важно, что toonote, hello узел структуру может сформированный XML. Поэтому при разработке сопоставления OData применяются корневая, родительская и дочерняя схемы.

## <a name="ignored-elements"></a>Пропускаемые элементы
Здесь представлены Hello hello высокой уровня элементы языка CSDL (узлы XML), не будут toobe, используемые серверной hello Azure Marketplace во время импорта hello метаданных hello веб-службы. Они могут присутствовать, но будут пропущены.

| Элемент | Область |
| --- | --- |
| Элемент Using |узел Hello, подчиненные узлы и все атрибуты |
| Элемент Documentation |узел Hello, подчиненные узлы и все атрибуты |
| ComplexType |узел Hello, подчиненные узлы и все атрибуты |
| Элемент Association |узел Hello, подчиненные узлы и все атрибуты |
| Свойство Extended |узел Hello, подчиненные узлы и все атрибуты |
| EntityContainer |Только для hello следующие атрибуты учитываются: *расширяет* и *AssociationSet* |
| Схема |Только для hello следующие атрибуты учитываются: *пространства имен* |
| FunctionImport |Только для hello следующие атрибуты учитываются: *режим* (значение по умолчанию функции LN предполагается) |
| EntityType |Только для hello следующие подчиненные узлы игнорируются: *ключ* и *PropertyRef* |

Hello ниже описаны toohello hello изменения (добавлены и учитываются элементы) различных узлов CSDL XML подробно.

## <a name="functionimport-node"></a>Узел FunctionImport
Узел FunctionImport представляет один URL-адрес (точка входа), предоставляющего конечным пользователем toohello службы. узел «Hello» позволяет описывающие способ обращения hello URL-адрес, какие параметры будут доступны toohello для конечных пользователей и каким образом предоставляются эти параметры.

Подробные сведения об этом узле см. на странице [MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx).

Hello ниже приведены дополнительные атрибуты hello (или дополнения tooattributes), предоставляемые hello FunctionImport узла:

**d:baseUri** -hello шаблон URI для ресурса REST hello, предоставляемый tooMarketplace. Marketplace использует hello шаблона tooconstruct запросы к веб-службы REST hello. шаблон URI Hello содержит заполнители для hello параметров в форме hello {parameterName}, где Имя_параметра hello имя параметра hello. Например, apiVersion={версия_API}.
Параметры допускаются tooappear как параметры URI или как часть пути URI hello. В случае hello внешнего вида hello в путь hello они всегда являются обязательными (не может быть помечен как допускающая значение NULL). *Пример:* `d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Имя** -имя hello hello импортированной функции.  Не может быть hello такой же, как другие имена, определенные в языке CSDL hello.  Например, Name="GetModelUsageFile".

**EntitySet** *(необязательно)* — Если функция hello возвращает коллекцию типов сущностей, значение hello hello **EntitySet** должен быть принадлежит коллекция hello toowhich набор сущностей hello. В противном случае hello **EntitySet** не следует использовать атрибут. *Пример:* `EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(необязательно)* -задает тип элементов, возвращаемых методом hello URI hello.  Не используйте этот атрибут, если функция hello не возвращает значение. Здесь представлены Hello hello поддерживаемые типы:

* **Collection (<Entity type name>)** — задает коллекцию определенных типов сущностей. Имя Hello присутствует в атрибуте Name hello hello EntityType узла. Например, Collection(WXC.HourlyResult).
* **Необработанный (<mime type>)**: указывает необработанные документа или большого двоичного объекта, возвращается toohello пользователя. Например, Raw(image/jpeg). Другие примеры:

  * ReturnType="Raw(text/plain)";
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*.

**d:Paging** -задает способ обработки разбиения на страницы с hello ресурс REST. Здравствуйте внутри фигурных ветвях используются значения параметров, например страница = {$page} & значение itemsperpage = доступные параметры: hello {$size}:

* **None** — разбиение на страницы недоступно.
* **Skip** — разбиение на страницы выражается с помощью логических значений skip и take (вверху). Пропустить перейдет элементами M и take, а затем возвращает hello Далее N-элементов. Значение параметра: $skip.
* **Take:** Take возвращает следующие N элементы hello. Значение параметра: $take.
* **PageSize** — разбиение на страницы выражается с помощью логических значений page и size (количество элементов на страницу). Страница представляет hello текущей страницы, которое возвращается. Значение параметра: $page.
* **Размер:** размер представляет hello количество элементов, возвращаемых для каждой страницы. Значение параметра: $size.

**d:AllowedHttpMethods** *(необязательно)* -указывает, какие команды обрабатывается ресурс REST hello. Также ограничивает принятые командой toohello указано значение.  По умолчанию используется POST.  *Пример:* `d:AllowedHttpMethods="GET"` hello вариантами являются:

* **GET:** обычно используется tooreturn данных
* **POST:** обычно используется tooinsert новых данных
* **PUT:** обычно используется tooupdate данных
* **УДАЛЕНИЕ:** используется toodelete данных

(Не соответствует ни hello CSDL документации) дополнительные дочерние узлы, в узле FunctionImport hello являются:

**d:RequestBody** *(необязательно)* -toobe тело отправляемых ожидает используется tooindicate, hello запроса — текст запроса hello. Параметры можно задать в теле запроса hello. Они задаются в фигурных скобках, например {parameterName}. Эти параметры сопоставляются из hello ввод данных пользователем в текст hello, который является перемещение toohello содержимого поставщика службы. Hello requestBody элемент имеет атрибут с именем httpMethod. атрибут Hello позволяет двух значений:

* **POST:** используется, если hello запрос HTTP POST
* **GET:** используется, если hello запрос HTTP GET

    Пример:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:Namespaces** и **d:Namespace** -hello пространств имен, определенных в hello XML, возвращаемый импортом функции hello (конечной точки URI) описывает этого узла. Hello XML, возвращаемый hello серверная служба может содержать любое количество пространств имен toodifferentiate hello содержимое, которое возвращается. **Все эти пространства имен, если использовать в запросах XPath d:Map или d:Match должны toobe в списке.** узел d:Namespaces Hello содержит набор или список d:Namespace узлов. Каждый из них перечислены одно пространство имен, используемое в ответе службы hello серверной части. Здесь представлены Hello hello атрибута hello d:Namespace узла:

* **d:prefix:** hello префикс для пространства имен hello, как показано в hello XML результаты, возвращаемые службой hello, например f:FirstName, f:LastName, где f — префикс hello.
* **d:URI:** hello полный URI пространства имен hello, используемые в документе результат hello. Он представляет значение hello этот префикс hello — разрешить tooat среды выполнения.

**d:ErrorHandling** *(необязательно)* — узел содержит условия обработки ошибок. Каждое из условий hello проверяется hello результат, возвращаемый службой hello поставщика содержимого. Если условие соответствует hello код ошибки HTTP, предложенные сообщение об ошибке возвращается toohello для конечных пользователей.

**d:ErrorHandling** *(необязательно)* и **d:Condition** *(необязательно)* -узел условие содержит одно условие, возвращается hello результата, возвращаемого методом Служба Hello поставщика содержимого. Hello ниже приведены hello **необходимые** атрибуты:

* **d:Match:** выражение XPath, которое проверяет, является ли данный узел значение присутствует в поставщик содержимого hello выходного XML. Hello XPath выполняется для вывода hello и должен возвращать значение true, если условие hello совпадение или false в противном случае.
* **d:HttpStatusCode:** hello код состояния HTTP, которое должно возвращаться Marketplace в условие соответствует hello вариантов hello. Marketplace signalizes пользователя toohello ошибок с помощью коды состояния HTTP. Список кодов состояния HTTP можно найти по адресу http://en.wikipedia.org/wiki/HTTP_status_code.
* **d:ErrorMessage:** hello сообщение об ошибке, возвращаемый — с кодом состояния hello HTTP — toohello для конечных пользователей. Это должно быть понятное сообщение об ошибке, не содержащее секретных данных.

**d:Title** *(необязательно)* -позволяющий описывать hello заголовок функции hello. значение заголовка hello Hello поступает из

* Hello карты необязательный атрибут (xpath) которого указывает, где toofind заголовок hello в ответ hello полученный запрос службы hello.
* - Или - title hello, указанный как значение узла hello.

**d:Rights** *(необязательно)* -hello (например об авторских правах) права, связанные с функции hello. значение Hello права hello поступает из:

* Hello карты необязательный атрибут (xpath) который указывает, где toofind права hello в ответ hello полученный запрос службы hello.
* - Или - hello права, указанные как значение узла hello.

**d:Description** *(необязательно)* — краткое описание функции hello. значение Hello для описания hello поступает из

* Hello карты необязательный атрибут (xpath) которого указывает, где toofind описание hello в ответ hello возвращаться из запроса на обслуживание hello.
* - Или -описание hello, указанный как значение узла hello.

**d:EmitSelfLink** - *см. пример выше «FunctionImport для разбиения возвращаемых данных на страницы»*

**d:EncodeParameterValue** -tooOData дополнительное расширение

**d:QueryResourceCost** -tooOData дополнительное расширение

**d:map** -tooOData дополнительное расширение

**d:Headers** -tooOData дополнительное расширение

**d:Headers** -tooOData дополнительное расширение

**d:value** -tooOData дополнительное расширение

**d:HttpStatusCode** -tooOData дополнительное расширение

**d:ErrorMessage** -tooOData дополнительное расширение

## <a name="parameter-node"></a>Узел параметра
Этот узел представляет один параметр, который предоставляется как часть шаблона URI hello / текст, который был задан в узле FunctionImport hello запроса.

Посетите страницу документа очень полезные сведения об узле «Элемент параметра» hello [здесь](http://msdn.microsoft.com/library/ee473431.aspx) (используйте hello **другие версии** tooselect раскрывающийся список другой версии, если необходимые tooview hello документации). *Пример:* `<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Атрибут параметра | Обязательный | Значение |
| --- | --- | --- |
| Имя |Да |Имя параметра hello Hello. Учитывается регистр.  Учитывать регистр BaseUri hello. **Пример:** `<Property Name="IsDormant" Type="Byte" />` |
| Тип |Да |Тип параметра Hello. Hello значение должно быть **EDMSimpleType** или сложный тип, который находится в пределах области hello hello модели. Дополнительные сведения см. в разделе «6 поддерживаемых параметров и типов свойств».  (Учитывается регистр. Первый символ — прописная буква, все остальные — строчные.)  Дополнительные сведения см. в статье [Типы концептуальной модели (CSDL)] ([MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx)). **Пример:** `<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |Нет |**В**, Out или InOut, в зависимости от того, является ли параметр hello входные, выходные или параметра ввода вывода. (В Azure Marketplace доступен только In.) **Пример:** `<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |Нет |Hello максимально допустимая длина параметра hello. **Пример:** `<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precision |Нет |Точность параметра hello Hello. **Пример:** `<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Масштаб |Нет |Масштаб параметра hello Hello. **Пример:** `<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Здесь представлены Hello hello атрибутов, которые были добавлены спецификация языка CSDL toohello:

| Атрибут параметра | Описание |
| --- | --- |
| **d:Regex** *(необязательно)* |Инструкция регулярное выражение используется toovalidate hello входное значение для параметра hello. Если входное значение hello не соответствует значению hello инструкции hello отклоняется. Это позволяет toospecify также набор возможных значений, например ^ [0-9] +? $ tooonly допускает номера. **Пример:** `<Parameter Name="имя" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="Имя, которое не может содержать пробелы, цифры или знаки, не входящие в латинский алфавит" d:SampleValues="George |
| **d:Enum** *(необязательно)* |Список значений, допустимых для параметра hello через канал. Тип значений, hello Hello должен toomatch hello определенный тип параметра hello. Пример: `english |
| **d: Nullable** *(необязательно)* |Позволяет определить, может ли параметр иметь значение NULL. по умолчанию Hello: true. Тем не менее, предоставляемых как часть пути hello в шаблоне URI hello не может принимать значение null. Если hello атрибуту значение toofalse для этих параметров — переопределяется hello ввод данных пользователем. **Пример:** `<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(необязательно)* |Пример значения toodisplay как Примечание toohello клиента в hello пользовательского интерфейса.  Можно вывести список tooadd запятыми несколько значений, используя символ вертикальной черты, т. е. " |

## <a name="entitytype-node"></a>Узел EntityType
Этот узел представляет один из типов hello, возвращаемых из Marketplace toohello конечного пользователя. Он также содержит сопоставление hello hello выходные данные, возвращаемые hello содержимого поставщика службы toohello значения, возвращаемые toohello для конечных пользователей.

Подробные сведения об этом узле находятся в [здесь](http://msdn.microsoft.com/library/bb399206.aspx) (используйте hello **другие версии** tooselect раскрывающийся список другой версии, если необходимые tooview hello документации.)

| Имя атрибута | Обязательный | Значение |
| --- | --- | --- |
| Имя |Да |Имя типа сущности hello Hello. **Пример:** `<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |Нет |имя другого типа сущности, который является базовым типом hello hello типа сущности, которая определена в Hello. **Пример:** `<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Здесь представлены Hello hello атрибутов, которые были добавлены спецификация языка CSDL toohello:

**d:map** -выражение XPath, выполняется к выходным данным службы hello. Hello здесь предполагается, что вывод службы hello содержит набор элементов, которые повторяются, как where веб-канал ATOM имеется набор узлов запись, которые повторяются. Каждый из повторяющихся узлов содержит одну запись. Hello XPath является, то указанный toopoint в отдельных повторяющийся узел hello в результате hello содержимого поставщика службы, который содержит значения hello отдельную запись. Пример выходных данных из службы hello.

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Hello выражение XPath должно быть /foo/bar, потому что каждый узел панели hello — hello, повторяющиеся выходные данные узла в hello и содержит фактическое содержимое hello, возвращаемый toohello для конечных пользователей.

**Key** — Marketplace пропускает этот атрибут. Веб-службы на основе REST обычно не предоставляют первичный ключ.

## <a name="property-node"></a>Узел Property
Этот узел содержит одно свойство записи hello.

Подробные сведения об этом узле находятся в [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (используйте hello **другие версии** tooselect раскрывающийся список другой версии, если необходимые tooview hello документации.) *Пример:* `<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | обязательные | Значение |
| --- | --- | --- |
| Имя |Да |Имя свойства hello Hello. |
| Тип |Да |Тип значения свойства hello Hello. должен быть тип значения свойства Hello **EDMSimpleType** или сложный тип (изображается полное доменное имя), который находится в пределах области hello модели. Дополнительные сведения см. в разделе «Типы концептуальной модели». |
| Nullable |Нет |**Значение true,** (hello значение по умолчанию) или **False** в зависимости от того, является ли свойство hello может иметь значение null. Примечание: В hello версия CSDL определяется hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) пространства имен, свойство сложного типа должно иметь Nullable = «False». |
| DefaultValue |Нет |значение по умолчанию Hello hello свойства. |
| MaxLength |Нет |Hello Максимальная длина значения свойства hello. |
| FixedLength |Нет |**Значение true,** или **False** в зависимости от значения свойства hello будет храниться как строку fiexed длины. |
| Precision |Нет |Указывает максимальное число toohello tooretain цифр в числовое значение hello. |
| Масштаб |Нет |Максимальное количество десятичных разрядов tooretain hello числовое значение. |
| Unicode |Нет |**Значение true,** или **False** в зависимости от того, будет ли значение свойства hello хранятся в виде строки в Юникоде. |
| Collation |Нет |Строка, указывающая hello упорядочивания toobe последовательности, используемое в источнике данных hello. |
| ConcurrencyMode |Нет |**Нет** (hello значение по умолчанию) или **Fixed**. Если значение hello задано слишком**Fixed**, значение свойства hello будет использоваться в проверках на оптимистичный параллелизм. |

Здесь представлены Hello hello дополнительные атрибуты, которые были добавлены toohello спецификация языка CSDL:

**d:map** -выражение XPath, выполняется для службы hello выходные и извлекает одно свойство hello выходных данных. Hello указан XPath — относительный toohello повторяющийся узел, который был выбран в hello EntityType узлов XPath. Это также возможно toospecify абсолютный tooallow XPath, включая статический ресурс в каждом hello выходных узлов, таких как, например заявление об авторских правах, находящийся только в том случае, когда в hello выходных данных для исходной службы, но должны присутствовать в каждой из строк hello в hello OData выходные данные. Пример из службы hello.

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

выражение XPath Hello здесь будет ./bar/baz0 tooget hello baz0 узел из hello содержимого поставщика службы.

**d:CharMaxLength** -для строкового типа, вы можете указать hello максимальной длины. См. пример DataService CSDL.

**d:IsPrimaryKey** -указывает, является ли столбец hello hello первичный ключ в hello таблицы или представления. См. пример DataService CSDL.

**d:isExposed** -определяет, если схема таблицы hello (обычно true). См. пример DataService CSDL.

**d:IsView** *(необязательно)* — задается значение True, если основывается на представлении, а не на таблице.  См. пример DataService CSDL.

**d:Tableschema** — см. пример DataService CSDL.

**d:ColumnName** -hello имя столбца hello в hello таблицы или представления.  См. пример DataService CSDL.

**d:IsReturned** -— логическое значение, определяющее, если hello службы предоставляет этот клиент toohello значение hello.  См. пример DataService CSDL.

**d:IsQueryable** -— hello логическое значение, определяющее, если столбец hello может использоваться в запрос к базе данных.   См. пример DataService CSDL.

**d:OrdinalPosition** -является столбец hello числовая позиция внешний вид, x, hello таблицы или представления hello, где x — от 1 toohello число столбцов в таблице hello.  См. пример DataService CSDL.

**d:DatabaseDataType** -тип данных hello hello столбца в базе данных hello, т. е. тип данных SQL. См. пример DataService CSDL.

## <a name="supported-parametersproperty-types"></a>Поддерживаемые типы параметров и свойств
Здесь представлены Hello hello поддерживается типы параметров и свойств. (Учитывается регистр.)

| Примитивные типы | Описание |
| --- | --- |
| Null |Представляет hello отсутствия определенного значения |
| Логический |Представляет математическое понятие двоичной логики hello |
| Byte |8-разрядное целое значение без знака |
| DateTime |Представляет дату и время с диапазоном значений от 12:00:00 полночь 1 января 1753 г. н. э. до 11:59:59 пополудни, декабрь 9999 г. н. э. |
| Decimal |Представляет числовые значения с фиксированной точностью и масштабом. Этот тип может описывать числовые значения в диапазоне от отрицательного значения 10 ^ 255 + 1 toopositive 10 ^-255 1 |
| Double |Представляет число с плавающей запятой с точностью в 15 цифр, которое может представлять значения в диапазоне примерно от ±2.23e –308 до ±1.79e +308. **Использование десятичных из-за проблемы tooExel экспорта** |
| Single |Представляет число с плавающей запятой с точностью в 7 цифр, которое может представлять значения в диапазоне примерно от ± 1.18e -38 до ± 3.40e +38 |
| Guid |Представляет 16-байтовое (128-разрядное) значение уникального идентификатора |
| Int16 |Представляет 16-разрядное целое значение со знаком |
| Int32 |Представляет 32-разрядное целое значение со знаком |
| Int64 |Представляет 64-разрядное целое значение со знаком |
| Строка |Представляет символьные данные фиксированной или переменной длины |

## <a name="see-also"></a>См. также
* Если вы заинтересованы в общее представление о hello общий процесс сопоставления OData и цели, эта статья [данных службы OData сопоставления](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview определений, структуры и инструкции.
* Если вы заинтересованы в просмотре примеров, эта статья [примеры сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee образцы кода и понимания синтаксиса кода и контекста.
* Указанный путь для публикации toohello службы данных Azure Marketplace, эта статья toohello tooreturn [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).
