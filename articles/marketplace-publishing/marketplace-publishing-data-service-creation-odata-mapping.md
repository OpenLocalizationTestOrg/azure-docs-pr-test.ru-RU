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
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="5ba31-103">Сопоставление существующего tooOData службы web, через CSDL</span><span class="sxs-lookup"><span data-stu-id="5ba31-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5ba31-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="5ba31-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="5ba31-105">Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="5ba31-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="5ba31-106">Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="5ba31-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="5ba31-107">В данной статье приводится обзор о том, как toouse toomap CSDL существующей службы tooan совместимой службы OData.</span><span class="sxs-lookup"><span data-stu-id="5ba31-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="5ba31-108">Здесь объясняется, как toocreate hello документ сопоставления (CSDL), преобразующий hello входной запрос от клиента hello посредством вызова службы и hello вывода клиента toohello (данные) обратно через совместимых каналов OData.</span><span class="sxs-lookup"><span data-stu-id="5ba31-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="5ba31-109">Microsoft Azure Marketplace предоставляет конечным пользователям toohello службы с помощью протокола OData hello.</span><span class="sxs-lookup"><span data-stu-id="5ba31-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="5ba31-110">Службы, предоставляемые поставщиками содержимого (владельцами данных), представлены в различных формах, например REST, SOAP и т. д.</span><span class="sxs-lookup"><span data-stu-id="5ba31-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="5ba31-111">CSDL и его структура</span><span class="sxs-lookup"><span data-stu-id="5ba31-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="5ba31-112">CSDL (язык определения концептуальной схемы) представляет собой спецификацию, определение того, как toodescribe веб-службы или базы данных службы в общем toohello формулировки XML Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5ba31-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="5ba31-113">Краткий обзор hello **запроса потока:**</span><span class="sxs-lookup"><span data-stu-id="5ba31-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="5ba31-114">Hello **потока данных** в hello противоположного направления:</span><span class="sxs-lookup"><span data-stu-id="5ba31-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="5ba31-115">**Рис. 1** диаграммы, как клиент будет принимать данные от поставщика содержимого (службы) через hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5ba31-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="5ba31-116">Hello CSDL используется запросом hello сопоставления или преобразования компонент toohandle hello и данные проходят между службами и hello запрос клиента hello поставщика содержимого.</span><span class="sxs-lookup"><span data-stu-id="5ba31-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="5ba31-117">*Рисунок 1: Подробные поток из запроса поставщика toocontent клиента через Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="5ba31-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="5ba31-119">Основные сведения о Atom, Atom Pub и протокол OData hello, после которого hello сборки расширений Azure Marketplace см. в статье: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="5ba31-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="5ba31-120">Отрывок из верхнего ссылку: *«hello hello Open Data protocol (здесь и далее ссылка tooas OData) предназначен протокола tooprovide, основанные на REST для операций CRUD стиля (Создание, чтение, обновление и удаление) в виде служб данных с ресурсами. "Служба данных" — это конечная точка, в которой представлены данные из одной или нескольких "коллекций", в каждой из которых ноль или более "записей" состоят из типизированной пары "имя-значение". OData публикуются корпорацией Майкрософт в разделе стандартов OASIS (организация для hello продвижения стандартов структурированной информации), что все, кто хочет toocan создавать серверов, клиентов и средств без ограничениями или роялти.»*</span><span class="sxs-lookup"><span data-stu-id="5ba31-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="5ba31-121">Ниже перечислены три важных элемента, имеющие определяемый языка CSDL hello toobe</span><span class="sxs-lookup"><span data-stu-id="5ba31-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="5ba31-122">Hello **конечная точка** из hello поставщика услуг hello Web адрес (URI) службы hello</span><span class="sxs-lookup"><span data-stu-id="5ba31-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="5ba31-123">Hello **параметров данных** передается как входной toohello поставщика услуг hello определения параметров hello, отправляемых службе toohello поставщика содержимого вниз toohello тип данных.</span><span class="sxs-lookup"><span data-stu-id="5ba31-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="5ba31-124">**Схемы** hello данных, возвращаемых схема hello toohello запроса службы данных hello, доставляются службе hello поставщика содержимого, включая контейнера, коллекций и таблицам, переменные и столбцы и типы данных.</span><span class="sxs-lookup"><span data-stu-id="5ba31-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="5ba31-125">Следующая схема Hello приведен обзор hello поток, из которой hello клиент вводит hello OData инструкции (вызов toohello поставщика содержимого веб-служба) toogetting hello результаты/данные обратно.</span><span class="sxs-lookup"><span data-stu-id="5ba31-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="5ba31-127">Шаги:</span><span class="sxs-lookup"><span data-stu-id="5ba31-127">Steps:</span></span>
1. <span data-ttu-id="5ba31-128">Клиент отправляет запрос, через вызов службы с входные параметры, определенные в XML toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5ba31-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="5ba31-129">CSDL — используется toovalidate hello вызова службы.</span><span class="sxs-lookup"><span data-stu-id="5ba31-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="5ba31-130">Hello в формате вызов службы затем отправляется toohello служба поставщиков содержимого с hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5ba31-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="5ba31-131">Hello веб-служба выполняет и выполняет действие hello hello HTTP-команда (т. е. получить) hello данные возвращаются tooAzure Marketplace, где hello запросило данные (если таковые имеются) — предоставляет в формате XML toohello клиента с помощью hello сопоставление, определенное в hello CSDL.</span><span class="sxs-lookup"><span data-stu-id="5ba31-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="5ba31-132">Hello клиента отправляется hello данных (если таковые имеются) в формате XML или JSON</span><span class="sxs-lookup"><span data-stu-id="5ba31-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="5ba31-133">Определения</span><span class="sxs-lookup"><span data-stu-id="5ba31-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="5ba31-134">OData ATOM pub</span><span class="sxs-lookup"><span data-stu-id="5ba31-134">OData ATOM pub</span></span>
<span data-ttu-id="5ba31-135">Расширение toohello ATOM pub, где каждая запись представляет одну строку результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="5ba31-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="5ba31-136">часть содержимого Hello hello записи — значения hello улучшенные toocontain hello строки — как пары ключ-значение.</span><span class="sxs-lookup"><span data-stu-id="5ba31-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="5ba31-137">Дополнительные сведения можно найти здесь: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="5ba31-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="5ba31-138">CSDL — язык определения концептуальной схемы</span><span class="sxs-lookup"><span data-stu-id="5ba31-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="5ba31-139">Позволяет определять функции (SPROC) и сущности, предоставляемые через базу данных.</span><span class="sxs-lookup"><span data-stu-id="5ba31-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="5ba31-140">Дополнительные сведения приведены здесь: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="5ba31-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="5ba31-141">Нажмите кнопку hello **других версий** раскрывающийся список и выберите версию, если вы не видите hello статьи.</span><span class="sxs-lookup"><span data-stu-id="5ba31-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="5ba31-142">EDM — модель данных записи</span><span class="sxs-lookup"><span data-stu-id="5ba31-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="5ba31-143">Обзор: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="5ba31-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="5ba31-144">Предварительная версия: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="5ba31-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="5ba31-145">Типы данных: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="5ba31-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="5ba31-146">Hello ниже показан hello подробные левой tooRight поток, из которой hello клиент вводит hello OData инструкции (вызов toohello поставщика содержимого веб-служба) toogetting hello результаты/данные обратно:</span><span class="sxs-lookup"><span data-stu-id="5ba31-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![рисунок](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="5ba31-148">Основы языка CSDL</span><span class="sxs-lookup"><span data-stu-id="5ba31-148">CSDL Basics</span></span>
<span data-ttu-id="5ba31-149">CSDL (язык определения концептуальной схемы) представляет собой спецификацию, определение того, как toodescribe веб-службы или базы данных службы в общем toohello формулировки XML Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5ba31-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="5ba31-150">Описывает язык CSDL hello критических единиц, **делает возможным hello передавать данные из источника данных hello toohello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="5ba31-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="5ba31-151">Здесь описаны Hello основных частей.</span><span class="sxs-lookup"><span data-stu-id="5ba31-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="5ba31-152">Сведения интерфейса, описывающие все общедоступные функции (узел FunctionImport)</span><span class="sxs-lookup"><span data-stu-id="5ba31-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="5ba31-153">Сведения о типах данных для всех сообщений requests(input) и сообщений responses(outputs) (узлы EntityContainer, EntitySet и EntityType)</span><span class="sxs-lookup"><span data-stu-id="5ba31-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="5ba31-154">Данные о hello транспортного протокола toobe привязки используется (заголовок узла)</span><span class="sxs-lookup"><span data-stu-id="5ba31-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="5ba31-155">Сведения об адресе для поиска hello указан службы (атрибут BaseURI)</span><span class="sxs-lookup"><span data-stu-id="5ba31-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="5ba31-156">По сути hello CSDL представляет контракт независимый платформы и языка между запрашивающей стороны службы hello и поставщиком услуг hello.</span><span class="sxs-lookup"><span data-stu-id="5ba31-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="5ba31-157">С помощью языка CSDL hello, клиентское приложение может найти базы данных службы веб-службы и вызвать его функцию общедоступным.</span><span class="sxs-lookup"><span data-stu-id="5ba31-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="5ba31-158">Связанные CSDL tooa базы данных или коллекции</span><span class="sxs-lookup"><span data-stu-id="5ba31-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="5ba31-159">**Спецификация языка CSDL Hello**</span><span class="sxs-lookup"><span data-stu-id="5ba31-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="5ba31-160">CSDL — это грамматика XML для описания веб-служб.</span><span class="sxs-lookup"><span data-stu-id="5ba31-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="5ba31-161">самой спецификации Hello делится на четыре основных элемента: EntitySet, FunctionImport; Пространство имен и тип EntityType.</span><span class="sxs-lookup"><span data-stu-id="5ba31-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="5ba31-162">toomake проще toounderstand это абстракция позволяет связать таблицу tooa CSDL.</span><span class="sxs-lookup"><span data-stu-id="5ba31-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="5ba31-163">Помните!</span><span class="sxs-lookup"><span data-stu-id="5ba31-163">Remember;</span></span>

  <span data-ttu-id="5ba31-164">Язык CSDL представляет собой независимый платформы и языка контракт между hello **запрашивающей стороны службы** и hello **поставщика услуг**.</span><span class="sxs-lookup"><span data-stu-id="5ba31-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="5ba31-165">С помощью языка CSDL **клиент** может найти **веб-службу или службу базы данных** и вызвать любую из ее общедоступных **функций**.</span><span class="sxs-lookup"><span data-stu-id="5ba31-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="5ba31-166">Для типа службы данных hello четыре части языка CSDL можно рассматривать с точки зрения базы данных, таблиц, столбцов и хранимая процедура.</span><span class="sxs-lookup"><span data-stu-id="5ba31-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="5ba31-167">Они соотносятся следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5ba31-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="5ba31-168">EntityContainer ~= база данных;</span><span class="sxs-lookup"><span data-stu-id="5ba31-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="5ba31-169">EntitySet ~= таблица;</span><span class="sxs-lookup"><span data-stu-id="5ba31-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="5ba31-170">EntityType ~= столбцы;</span><span class="sxs-lookup"><span data-stu-id="5ba31-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="5ba31-171">FunctionImport ~= хранимая процедура;</span><span class="sxs-lookup"><span data-stu-id="5ba31-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="5ba31-172">**Допускаются команды HTTP**</span><span class="sxs-lookup"><span data-stu-id="5ba31-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="5ba31-173">GET-возвращает значения из базы данных hello (Возвращает коллекцию)</span><span class="sxs-lookup"><span data-stu-id="5ba31-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="5ba31-174">POST — использовать toopass данных tooand необязательные значения, возвращаемые из db hello (Создание новой записи в коллекции hello, возвращаемый идентификатор или URI)</span><span class="sxs-lookup"><span data-stu-id="5ba31-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="5ba31-175">Удалить — удаляет данные из hello DB (удаляет коллекцию)</span><span class="sxs-lookup"><span data-stu-id="5ba31-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="5ba31-176">PUT – обновляет данные в базе данных (замена или создание коллекции).</span><span class="sxs-lookup"><span data-stu-id="5ba31-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="5ba31-177">Документ метаданных и сопоставления</span><span class="sxs-lookup"><span data-stu-id="5ba31-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="5ba31-178">документ метаданных и сопоставления Hello является используется toomap, существующий веб-поставщик содержимого служб, чтобы представлены как веб-служба OData системой hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5ba31-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="5ba31-179">Он основан на языке CSDL и реализует несколько расширений tooCSDL tooaccommodate hello потребностей REST на основе веб-служб, доступных через Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5ba31-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="5ba31-180">Hello расширения можно найти на hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) пространства имен.</span><span class="sxs-lookup"><span data-stu-id="5ba31-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="5ba31-181">Ниже приведен пример hello CSDL: (копировать и вставить hello ниже примере CSDL в XML-редакторе и измените toomatch службы.</span><span class="sxs-lookup"><span data-stu-id="5ba31-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="5ba31-182">Вставьте в CSDL сопоставление вкладка "DataService" при создании службы в hello [портал публикации Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="5ba31-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="5ba31-183">**Условия:** Relating hello CSDL условия toohello [портал публикации](https://publish.windowsazure.com) условия пользовательского интерфейса (PPUI).</span><span class="sxs-lookup"><span data-stu-id="5ba31-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="5ba31-184">Предложите «Title» в hello PPUI относится tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="5ba31-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="5ba31-185">Слишком относится MyCompany в hello PPUI**отображаемое имя издателя** в hello [Центр разработчиков](http://dev.windows.com/registration?accountprogram=azure) пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="5ba31-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="5ba31-186">API относится tooa веб- или службы данных (план hello PPUI)</span><span class="sxs-lookup"><span data-stu-id="5ba31-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="5ba31-187">**Иерархия.** Компания (поставщик содержимого) владеет предложениями, которые включают планы, а именно службы, которые адаптированы к API.</span><span class="sxs-lookup"><span data-stu-id="5ba31-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="5ba31-188">Пример WebService CSDL</span><span class="sxs-lookup"><span data-stu-id="5ba31-188">WebService CSDL Example</span></span>
<span data-ttu-id="5ba31-189">Подключается tooa службы, которая предоставление конечной точки веб-приложения (например, приложение C#)</span><span class="sxs-lookup"><span data-stu-id="5ba31-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

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
> <span data-ttu-id="5ba31-190">Просмотреть дополнительные примеры CSDL веб-службы в статье hello [примеры сопоставления существующей веб-службы tooOData через CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="5ba31-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="5ba31-191">Пример DataService CSDL</span><span class="sxs-lookup"><span data-stu-id="5ba31-191">DataService CSDL Example</span></span>
<span data-ttu-id="5ba31-192">Подключение службы tooa точкой базы данных таблицы или представления, как конечную точку в следующем примере показаны два API-интерфейсы для базы данных на основе CSDL API (можно использовать представления, а не таблиц).</span><span class="sxs-lookup"><span data-stu-id="5ba31-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

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

## <a name="see-also"></a><span data-ttu-id="5ba31-193">См. также</span><span class="sxs-lookup"><span data-stu-id="5ba31-193">See Also</span></span>
* <span data-ttu-id="5ba31-194">Если вы заинтересованы в обучении и основные сведения о hello конкретных узлов и их параметров, эта статья [узлы сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) для определения и объяснения, примеры и контекст вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="5ba31-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="5ba31-195">Если вы заинтересованы в просмотре примеров, эта статья [примеры сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee образцы кода и понимания синтаксиса кода и контекста.</span><span class="sxs-lookup"><span data-stu-id="5ba31-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="5ba31-196">Указанный путь для публикации toohello службы данных Azure Marketplace, эта статья toohello tooreturn [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="5ba31-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

