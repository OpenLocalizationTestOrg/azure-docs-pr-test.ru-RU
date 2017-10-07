---
title: "aaaGuide toocreating службы данных для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развертывать службу данных для приобретения на hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Сопоставление существующего tooOData службы web, через CSDL
> [!IMPORTANT]
> **В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.** Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners). Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

В данной статье приводится обзор о том, как toouse toomap CSDL существующей службы tooan совместимой службы OData. Здесь объясняется, как toocreate hello документ сопоставления (CSDL), преобразующий hello входной запрос от клиента hello посредством вызова службы и hello вывода клиента toohello (данные) обратно через совместимых каналов OData. Microsoft Azure Marketplace предоставляет конечным пользователям toohello службы с помощью протокола OData hello. Службы, предоставляемые поставщиками содержимого (владельцами данных), представлены в различных формах, например REST, SOAP и т. д.

## <a name="what-is-a-csdl-and-its-structure"></a>CSDL и его структура
CSDL (язык определения концептуальной схемы) представляет собой спецификацию, определение того, как toodescribe веб-службы или базы данных службы в общем toohello формулировки XML Azure Marketplace.

Краткий обзор hello **запроса потока:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Hello **потока данных** в hello противоположного направления:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Рис. 1** диаграммы, как клиент будет принимать данные от поставщика содержимого (службы) через hello Azure Marketplace.  Hello CSDL используется запросом hello сопоставления или преобразования компонент toohandle hello и данные проходят между службами и hello запрос клиента hello поставщика содержимого.

*Рисунок 1: Подробные поток из запроса поставщика toocontent клиента через Azure Marketplace*

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Основные сведения о Atom, Atom Pub и протокол OData hello, после которого hello сборки расширений Azure Marketplace см. в статье: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

Отрывок из верхнего ссылку: *«hello hello Open Data protocol (здесь и далее ссылка tooas OData) предназначен протокола tooprovide, основанные на REST для операций CRUD стиля (Создание, чтение, обновление и удаление) в виде служб данных с ресурсами. "Служба данных" — это конечная точка, в которой представлены данные из одной или нескольких "коллекций", в каждой из которых ноль или более "записей" состоят из типизированной пары "имя-значение". OData публикуются корпорацией Майкрософт в разделе стандартов OASIS (организация для hello продвижения стандартов структурированной информации), что все, кто хочет toocan создавать серверов, клиентов и средств без ограничениями или роялти.»*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Ниже перечислены три важных элемента, имеющие определяемый языка CSDL hello toobe
* Hello **конечная точка** из hello поставщика услуг hello Web адрес (URI) службы hello
* Hello **параметров данных** передается как входной toohello поставщика услуг hello определения параметров hello, отправляемых службе toohello поставщика содержимого вниз toohello тип данных.
* **Схемы** hello данных, возвращаемых схема hello toohello запроса службы данных hello, доставляются службе hello поставщика содержимого, включая контейнера, коллекций и таблицам, переменные и столбцы и типы данных.

Следующая схема Hello приведен обзор hello поток, из которой hello клиент вводит hello OData инструкции (вызов toohello поставщика содержимого веб-служба) toogetting hello результаты/данные обратно.

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>Шаги:
1. Клиент отправляет запрос, через вызов службы с входные параметры, определенные в XML toohello Azure Marketplace
2. CSDL — используется toovalidate hello вызова службы.
   * Hello в формате вызов службы затем отправляется toohello служба поставщиков содержимого с hello Azure Marketplace
3. Hello веб-служба выполняет и выполняет действие hello hello HTTP-команда (т. е. получить) hello данные возвращаются tooAzure Marketplace, где hello запросило данные (если таковые имеются) — предоставляет в формате XML toohello клиента с помощью hello сопоставление, определенное в hello CSDL.
4. Hello клиента отправляется hello данных (если таковые имеются) в формате XML или JSON

## <a name="definitions"></a>Определения
### <a name="odata-atom-pub"></a>OData ATOM pub
Расширение toohello ATOM pub, где каждая запись представляет одну строку результирующего набора. часть содержимого Hello hello записи — значения hello улучшенные toocontain hello строки — как пары ключ-значение. Дополнительные сведения можно найти здесь: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL — язык определения концептуальной схемы
Позволяет определять функции (SPROC) и сущности, предоставляемые через базу данных. Дополнительные сведения приведены здесь: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Нажмите кнопку hello **других версий** раскрывающийся список и выберите версию, если вы не видите hello статьи.
> 
> 

### <a name="edm---entry-data-model"></a>EDM — модель данных записи
* Обзор: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Предварительная версия: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Типы данных: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Hello ниже показан hello подробные левой tooRight поток, из которой hello клиент вводит hello OData инструкции (вызов toohello поставщика содержимого веб-служба) toogetting hello результаты/данные обратно:

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Основы языка CSDL
CSDL (язык определения концептуальной схемы) представляет собой спецификацию, определение того, как toodescribe веб-службы или базы данных службы в общем toohello формулировки XML Azure Marketplace. Описывает язык CSDL hello критических единиц, **делает возможным hello передавать данные из источника данных hello toohello Azure Marketplace.** Здесь описаны Hello основных частей.

* Сведения интерфейса, описывающие все общедоступные функции (узел FunctionImport)
* Сведения о типах данных для всех сообщений requests(input) и сообщений responses(outputs) (узлы EntityContainer, EntitySet и EntityType)
* Данные о hello транспортного протокола toobe привязки используется (заголовок узла)
* Сведения об адресе для поиска hello указан службы (атрибут BaseURI)

По сути hello CSDL представляет контракт независимый платформы и языка между запрашивающей стороны службы hello и поставщиком услуг hello. С помощью языка CSDL hello, клиентское приложение может найти базы данных службы веб-службы и вызвать его функцию общедоступным.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Связанные CSDL tooa базы данных или коллекции
**Спецификация языка CSDL Hello**

CSDL — это грамматика XML для описания веб-служб. самой спецификации Hello делится на четыре основных элемента: EntitySet, FunctionImport; Пространство имен и тип EntityType.

toomake проще toounderstand это абстракция позволяет связать таблицу tooa CSDL.

Помните!

  Язык CSDL представляет собой независимый платформы и языка контракт между hello **запрашивающей стороны службы** и hello **поставщика услуг**. С помощью языка CSDL **клиент** может найти **веб-службу или службу базы данных** и вызвать любую из ее общедоступных **функций**.

Для типа службы данных hello четыре части языка CSDL можно рассматривать с точки зрения базы данных, таблиц, столбцов и хранимая процедура.

Они соотносятся следующим образом:

* EntityContainer ~= база данных;
* EntitySet ~= таблица;
* EntityType ~= столбцы;
* FunctionImport ~= хранимая процедура;

**Допускаются команды HTTP**

* GET-возвращает значения из базы данных hello (Возвращает коллекцию)
* POST — использовать toopass данных tooand необязательные значения, возвращаемые из db hello (Создание новой записи в коллекции hello, возвращаемый идентификатор или URI)
* Удалить — удаляет данные из hello DB (удаляет коллекцию)
* PUT – обновляет данные в базе данных (замена или создание коллекции).

## <a name="metadatamapping-document"></a>Документ метаданных и сопоставления
документ метаданных и сопоставления Hello является используется toomap, существующий веб-поставщик содержимого служб, чтобы представлены как веб-служба OData системой hello Azure Marketplace. Он основан на языке CSDL и реализует несколько расширений tooCSDL tooaccommodate hello потребностей REST на основе веб-служб, доступных через Azure Marketplace. Hello расширения можно найти на hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) пространства имен.

Ниже приведен пример hello CSDL: (копировать и вставить hello ниже примере CSDL в XML-редакторе и измените toomatch службы.  Вставьте в CSDL сопоставление вкладка "DataService" при создании службы в hello [портал публикации Azure Marketplace](https://publish.windowsazure.com)).

**Условия:** Relating hello CSDL условия toohello [портал публикации](https://publish.windowsazure.com) условия пользовательского интерфейса (PPUI).

* Предложите «Title» в hello PPUI относится tooMyWebOffer
* Слишком относится MyCompany в hello PPUI**отображаемое имя издателя** в hello [Центр разработчиков](http://dev.windows.com/registration?accountprogram=azure) пользовательского интерфейса
* API относится tooa веб- или службы данных (план hello PPUI)

**Иерархия.** Компания (поставщик содержимого) владеет предложениями, которые включают планы, а именно службы, которые адаптированы к API.

### <a name="webservice-csdl-example"></a>Пример WebService CSDL
Подключается tooa службы, которая предоставление конечной точки веб-приложения (например, приложение C#)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Просмотреть дополнительные примеры CSDL веб-службы в статье hello [примеры сопоставления существующей веб-службы tooOData через CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Пример DataService CSDL
Подключение службы tooa точкой базы данных таблицы или представления, как конечную точку в следующем примере показаны два API-интерфейсы для базы данных на основе CSDL API (можно использовать представления, а не таблиц).

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>См. также
* Если вы заинтересованы в обучении и основные сведения о hello конкретных узлов и их параметров, эта статья [узлы сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) для определения и объяснения, примеры и контекст вариантов использования.
* Если вы заинтересованы в просмотре примеров, эта статья [примеры сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee образцы кода и понимания синтаксиса кода и контекста.
* Указанный путь для публикации toohello службы данных Azure Marketplace, эта статья toohello tooreturn [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).

