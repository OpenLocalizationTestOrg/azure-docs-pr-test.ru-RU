---
title: "Руководство по созданию службы данных для Marketplace | Документация Майкрософт"
description: "Подробные инструкции по созданию, сертификации и развертыванию службы данных для продажи в Azure Marketplace."
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
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="e9bf0-103">Примеры сопоставления существующей веб-службы OData через CSDL</span><span class="sxs-lookup"><span data-stu-id="e9bf0-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9bf0-104">**В настоящее время мы больше не подключаем новые издатели служб данных. Новые службы данных не будут утверждены для добавления в список.**</span><span class="sxs-lookup"><span data-stu-id="e9bf0-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="e9bf0-105">Дополнительные сведения о публикации бизнес-приложения SaaS на AppSource см. [здесь](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="e9bf0-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="e9bf0-106">Дополнительные сведения о публикации приложений IaaS или службы разработчика в Azure Marketplace см. [здесь](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="e9bf0-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="e9bf0-107">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "POST"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="e9bf0-108">Используйте "POST" для необработанных данных, чтобы создать новый подчиненный элемент и вернуть определенный сервером URL-адрес (расположение) или обновить часть подчиненного элемента по определенному сервером URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="e9bf0-109">Где подчиненный элемент — поток,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="e9bf0-110">т. е. неструктурированный,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-110">unstructured, ex.</span></span> <span data-ttu-id="e9bf0-111">например текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-111">a text file.</span></span>  <span data-ttu-id="e9bf0-112">Имейте в виду, что "POST" не идемпотентен без местоположения.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-112">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="e9bf0-113">Пример: FunctionImport с помощью "DELETE"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="e9bf0-114">Используйте "DELETE" для удаления указанного URI.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-114">Use DELETE to remove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="e9bf0-115">Пример: FunctionImport с помощью "POST"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="e9bf0-116">Используйте "POST" для необработанных данных, чтобы создать новый подчиненный элемент и вернуть определенный сервером URL-адрес (расположение) или обновить часть подчиненного элемента по определенному сервером URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="e9bf0-117">Где подчиненный элемент — структура.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="e9bf0-118">Имейте в виду, что "POST" не идемпотентен без местоположения.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-118">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="e9bf0-119">Пример: FunctionImport с помощью "PUT"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="e9bf0-120">Используйте "PUT", чтобы создать новый подчиненный элемент или обновить весь подчиненный элемент по определенному сервером URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="e9bf0-121">Когда подчиненный элемент — это структура, метод PUT обладает свойством идемпотентности, поэтому несколько вхождений дадут одно состояние,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="e9bf0-122">т. е. x = 5.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-122">x=5.</span></span>  <span data-ttu-id="e9bf0-123">"PUT" следует использовать с полным содержимым указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-123">Put should be used with the full content of the specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="e9bf0-124">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "PUT"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="e9bf0-125">Используйте "PUT" для необработанных данных, чтобы создать новый подчиненный элемент или обновить весь подчиненный элемент по определенному сервером URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="e9bf0-126">Где подчиненный элемент — поток,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="e9bf0-127">т. е. неструктурированный,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-127">unstructured, ex.</span></span> <span data-ttu-id="e9bf0-128">например текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-128">a text file.</span></span>  <span data-ttu-id="e9bf0-129">Метод PUT обладает свойством идемпотентности, поэтому несколько вхождений дадут одно состояние,</span><span class="sxs-lookup"><span data-stu-id="e9bf0-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="e9bf0-130">т. е. x = 5.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-130">x=5.</span></span>  <span data-ttu-id="e9bf0-131">"PUT" следует использовать с полным содержимым указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-131">Put should be used with the full content of the specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="e9bf0-132">Пример: FunctionImport для "необработанных" данных, возвращаемых с помощью "GET"</span><span class="sxs-lookup"><span data-stu-id="e9bf0-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="e9bf0-133">Используйте "GET" для необработанных данных, чтобы вернуть неструктурированный подчиненный элемент.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="e9bf0-134">Пример: FunctionImport для "разбиения на страницы" возвращаемых данных</span><span class="sxs-lookup"><span data-stu-id="e9bf0-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="e9bf0-135">Реализуйте разбиение по страницам RESTful для ваших данных вместе с GET.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="e9bf0-136">Разбиение по страницам по умолчанию равно 100 строкам данных на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-136">Default paging is set to 100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="e9bf0-137">См. также</span><span class="sxs-lookup"><span data-stu-id="e9bf0-137">See Also</span></span>
* <span data-ttu-id="e9bf0-138">Если вы хотите понять процесс и смысл сопоставления OData, см. статью [Сопоставление существующей веб-службы и OData с помощью CSDL](marketplace-publishing-data-service-creation-odata-mapping.md), где приводятся определения, структуры и инструкции.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="e9bf0-139">Если вы заинтересованы в изучении и понимании конкретных узлов и их параметров, в статье [Узлы сопоставления службы данных OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) вы найдете определения и объяснения, примеры и контекст вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="e9bf0-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="e9bf0-140">Чтобы вернуться к указанному пути для публикации службы данных в Azure Marketplace, см. [руководство по публикации службы данных](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="e9bf0-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

