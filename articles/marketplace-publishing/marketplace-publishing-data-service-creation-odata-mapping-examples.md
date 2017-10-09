---
title: "aaaGuide toocreating службы данных для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развертывать службу данных для приобретения на hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="dc29c-103">Примеры сопоставления существующей веб-службы tooOData через CSDLs</span><span class="sxs-lookup"><span data-stu-id="dc29c-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dc29c-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="dc29c-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="dc29c-105">Если у вас есть бизнес-приложений SaaS хотелось бы toopublish Дополнительные сведения можно найти на AppSource [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="dc29c-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="dc29c-106">Если у вас есть приложениях IaaS или разработчик службы вы бы как toopublish в Azure Marketplace можно найти дополнительные сведения о [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="dc29c-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="dc29c-107">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "POST"</span><span class="sxs-lookup"><span data-stu-id="dc29c-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="dc29c-108">Использовать новый подчиненный toocreate POST необработанные данные и возвращает свой сервер URL(location) tooupdate часть hello подчиненного сервера hello определенная или URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc29c-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="dc29c-109">Где hello подчиненный объект — потока, т. е. неструктурированных ex.</span><span class="sxs-lookup"><span data-stu-id="dc29c-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="dc29c-110">например текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="dc29c-110">a text file.</span></span>  <span data-ttu-id="dc29c-111">Имейте в виду, что "POST" не идемпотентен без местоположения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-111">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="dc29c-112">Пример: FunctionImport с помощью "DELETE"</span><span class="sxs-lookup"><span data-stu-id="dc29c-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="dc29c-113">Используйте tooremove удалить указанный универсальный код Ресурса.</span><span class="sxs-lookup"><span data-stu-id="dc29c-113">Use DELETE tooremove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="dc29c-114">Пример: FunctionImport с помощью "POST"</span><span class="sxs-lookup"><span data-stu-id="dc29c-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="dc29c-115">Использовать новый подчиненный toocreate POST необработанные данные и возвращает свой сервер URL(location) tooupdate часть hello подчиненного сервера hello определенная или URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc29c-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="dc29c-116">Где hello подчиненный объект — это структура.</span><span class="sxs-lookup"><span data-stu-id="dc29c-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="dc29c-117">Имейте в виду, что "POST" не идемпотентен без местоположения.</span><span class="sxs-lookup"><span data-stu-id="dc29c-117">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="dc29c-118">Пример: FunctionImport с помощью "PUT"</span><span class="sxs-lookup"><span data-stu-id="dc29c-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="dc29c-119">Использовать новый подчиненный PUT toocreate или tooupdate hello всей подчиненный объект на сервере определен URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc29c-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="dc29c-120">Где hello подчиненный объект — это структура, PUT является идемпотентной, поэтому несколько вхождений приведет к hello же состояние, т. е.</span><span class="sxs-lookup"><span data-stu-id="dc29c-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="dc29c-121">т. е. x = 5.</span><span class="sxs-lookup"><span data-stu-id="dc29c-121">x=5.</span></span>  <span data-ttu-id="dc29c-122">PUT должен использоваться с hello hello указано полное содержимое ресурса.</span><span class="sxs-lookup"><span data-stu-id="dc29c-122">Put should be used with hello full content of hello specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="dc29c-123">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "PUT"</span><span class="sxs-lookup"><span data-stu-id="dc29c-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="dc29c-124">Использовать новый подчиненный ПОМЕСТИТЬ необработанных данных toocreate или tooupdate hello всей подчиненный объект на сервере определенных URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="dc29c-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="dc29c-125">Где hello подчиненный объект — потока, т. е. неструктурированных ex.</span><span class="sxs-lookup"><span data-stu-id="dc29c-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="dc29c-126">например текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="dc29c-126">a text file.</span></span>  <span data-ttu-id="dc29c-127">PUT является идемпотентным, поэтому несколько вхождений приведет к hello же состояние, т. е.</span><span class="sxs-lookup"><span data-stu-id="dc29c-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="dc29c-128">т. е. x = 5.</span><span class="sxs-lookup"><span data-stu-id="dc29c-128">x=5.</span></span>  <span data-ttu-id="dc29c-129">PUT должен использоваться с hello hello указано полное содержимое ресурса.</span><span class="sxs-lookup"><span data-stu-id="dc29c-129">Put should be used with hello full content of hello specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="dc29c-130">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "GET"</span><span class="sxs-lookup"><span data-stu-id="dc29c-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="dc29c-131">Используйте получить необработанные данные tooreturn подчиненный, неструктурированных, т. е. текст.</span><span class="sxs-lookup"><span data-stu-id="dc29c-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="dc29c-132">Пример: FunctionImport для "разбиения на страницы" возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="dc29c-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="dc29c-133">Реализуйте разбиение по страницам RESTful для ваших данных вместе с GET.</span><span class="sxs-lookup"><span data-stu-id="dc29c-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="dc29c-134">Разбиение на страницы по умолчанию имеет значение too100 строку на каждую страницу данных.</span><span class="sxs-lookup"><span data-stu-id="dc29c-134">Default paging is set too100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="dc29c-135">См. также</span><span class="sxs-lookup"><span data-stu-id="dc29c-135">See Also</span></span>
* <span data-ttu-id="dc29c-136">Если вы заинтересованы в общее представление о hello общий процесс сопоставления OData и цели, эта статья [данных службы OData сопоставления](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview определений, структуры и инструкции.</span><span class="sxs-lookup"><span data-stu-id="dc29c-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="dc29c-137">Если вы заинтересованы в обучении и основные сведения о hello конкретных узлов и их параметров, эта статья [узлы сопоставление данных службы OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) для определения и объяснения, примеры и контекст вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="dc29c-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="dc29c-138">Указанный путь для публикации toohello службы данных Azure Marketplace, эта статья toohello tooreturn [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="dc29c-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

