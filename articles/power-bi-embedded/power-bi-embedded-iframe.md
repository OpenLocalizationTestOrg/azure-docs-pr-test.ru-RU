---
title: "Power BI Embedded с ОСТАЛЬНОЙ toouse aaaHow | Документы Microsoft"
description: "Узнайте, как toouse Power BI Embedded с REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="60895-103">Как toouse Power BI Embedded с REST</span><span class="sxs-lookup"><span data-stu-id="60895-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="60895-104">Power BI Embedded: что это такое и как это использовать</span><span class="sxs-lookup"><span data-stu-id="60895-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="60895-105">Общие сведения о Power BI Embedded описан в официальное hello [Power BI Embedded сайта](https://azure.microsoft.com/services/power-bi-embedded/), но давайте рассмотрим это быстрый, прежде чем мы перейдем hello сведения об использовании REST.</span><span class="sxs-lookup"><span data-stu-id="60895-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="60895-106">На самом деле все довольно просто.</span><span class="sxs-lookup"><span data-stu-id="60895-106">It's quite simple, really.</span></span> <span data-ttu-id="60895-107">Вы можете toouse hello динамических данных визуализации [Power BI](https://powerbi.microsoft.com) в приложении.</span><span class="sxs-lookup"><span data-stu-id="60895-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="60895-108">Большинство пользовательских приложений требуется toodeliver hello данных для своих клиентов, не обязательно пользователей в их собственных организации.</span><span class="sxs-lookup"><span data-stu-id="60895-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="60895-109">Например если какой-либо службой для компании A и B компании программным обеспечением, пользователи в организации A должны видеть только данные для своих собственных компании A. То есть hello многопользовательский режим необходим для доставки hello.</span><span class="sxs-lookup"><span data-stu-id="60895-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="60895-110">пользовательское приложение Hello может также предложения свои собственные методы проверки подлинности, например форм проверки подлинности, обычная проверка подлинности и т.д...</span><span class="sxs-lookup"><span data-stu-id="60895-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="60895-111">Затем hello внедрения решения необходимо работать совместно с этого существующие методы проверки подлинности безопасно.</span><span class="sxs-lookup"><span data-stu-id="60895-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="60895-112">Это также может потребоваться для пользователей toobe может toouse hello этих приложений независимых поставщиков программного обеспечения, без дополнительных покупки или лицензирования подписки Power BI.</span><span class="sxs-lookup"><span data-stu-id="60895-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="60895-113">Служба **Power BI Embedded** разработана именно для такого рода сценариев.</span><span class="sxs-lookup"><span data-stu-id="60895-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="60895-114">Таким образом теперь, когда у нас есть, краткие сведения за пределы hello способом, давайте получить некоторые сведения о</span><span class="sxs-lookup"><span data-stu-id="60895-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="60895-115">Можно использовать hello .NET \(C#) или Node.js SDK tooeasily построить приложение с Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="60895-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="60895-116">Но в этой статье мы рассмотрим, как создать поток HTTP \(включая AuthN) Power BI без использования пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="60895-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="60895-117">Основные сведения об этой процедуре, можно построить приложение **с любым языком программирования**, и можно понять, глубоко hello суть Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="60895-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="60895-118">Создание коллекции рабочих областей Power BI и получение ключа доступа \(подготовка)</span><span class="sxs-lookup"><span data-stu-id="60895-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="60895-119">Power BI Embedded является одним из hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="60895-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="60895-120">Для использования сборов взимается только hello ISV, который использует портал Azure \(за каждый час сеанс пользователя), и пользователь hello, представления отчетов hello не сняты или даже требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="60895-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="60895-121">Перед началом нашей разработкой приложения, необходимо создать hello **коллекции рабочей области Power BI** с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="60895-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="60895-122">Каждой рабочей области Power BI Embedded является hello рабочей области для каждого клиента (клиента), и в каждой коллекции в рабочей области можно добавить несколько рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="60895-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="60895-123">Здравствуйте, ключ доступа используется в каждой коллекции в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="60895-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="60895-124">В силу коллекции hello рабочей области является границей безопасности hello для Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="60895-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="60895-125">После завершения создания коллекции hello рабочей области, скопируйте ключ доступа hello с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="60895-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="60895-126">Мы также подготовить коллекцию hello рабочей области и получить ключ доступа через REST API.</span><span class="sxs-lookup"><span data-stu-id="60895-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="60895-127">toolearn более, в разделе [API-интерфейсы поставщика ресурса Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="60895-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="60895-128">Создание PBIX-файла с помощью Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="60895-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="60895-129">Далее необходимо создать подключение к данным hello и внедренных toobe отчеты.</span><span class="sxs-lookup"><span data-stu-id="60895-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="60895-130">Эта задача не выполняется программно или с помощью кода.</span><span class="sxs-lookup"><span data-stu-id="60895-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="60895-131">Мы просто воспользуемся Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="60895-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="60895-132">В этой статье мы не будем останавливаться hello сведений о том, как toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="60895-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="60895-133">Дополнительные сведения по этому вопросу см. в руководстве [Начало работы с Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="60895-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="60895-134">В нашем примере мы просто используем hello [анализ розничной торговли](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="60895-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="60895-135">Создание рабочей области Power BI</span><span class="sxs-lookup"><span data-stu-id="60895-135">Create a Power BI workspace</span></span>

<span data-ttu-id="60895-136">Теперь, когда подготовка hello действия выполняются, давайте приступить к созданию рабочей области клиента в коллекции рабочей hello через интерфейсы API REST.</span><span class="sxs-lookup"><span data-stu-id="60895-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="60895-137">Hello следующие HTTP POST запроса (REST) является создание новой рабочей области hello в существующей коллекции рабочей области.</span><span class="sxs-lookup"><span data-stu-id="60895-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="60895-138">Это hello [POST рабочую область API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="60895-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="60895-139">В нашем примере является имя коллекции hello рабочей **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="60895-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="60895-140">Мы просто установите ключ доступа hello, который мы ранее скопировано, как **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="60895-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="60895-141">Это очень простая аутентификация!</span><span class="sxs-lookup"><span data-stu-id="60895-141">It’s very simple authentication!</span></span>

<span data-ttu-id="60895-142">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="60895-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="60895-143">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="60895-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="60895-144">Возвращаемый Hello **ИД рабочей области** используется для hello, следуя последующие вызовы API.</span><span class="sxs-lookup"><span data-stu-id="60895-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="60895-145">Это значение должно сохраниться в нашем приложении.</span><span class="sxs-lookup"><span data-stu-id="60895-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="60895-146">Импортировать pbix-файла в рабочей области hello</span><span class="sxs-lookup"><span data-stu-id="60895-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="60895-147">Каждый отчет в рабочей области соответствует tooa один файл Power BI Desktop с набором данных \(включая параметры источника данных).</span><span class="sxs-lookup"><span data-stu-id="60895-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="60895-148">Мы можем импортировать нашей .pbix файл toohello рабочей области, как показано в следующем примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="60895-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="60895-149">Как видите, могут загружаться hello двоичное pbix-файла с помощью составного сообщения MIME в http.</span><span class="sxs-lookup"><span data-stu-id="60895-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="60895-150">фрагмент uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello ИД рабочей области, а параметр запроса **datasetDisplayName** — toocreate имя набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="60895-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="60895-151">Hello создан набор данных содержит все данные, связанные hello артефактов в pbix-файл как импортированные данные источника данных toohello указатель, и т. д.</span><span class="sxs-lookup"><span data-stu-id="60895-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="60895-152">Выполнение этой задачи импорта может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="60895-152">This import task might run for a while.</span></span> <span data-ttu-id="60895-153">По завершении наше приложение может потребовать от состояния задачи hello, с помощью идентификатора импорта. В нашем примере — идентификатор hello импорта **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="60895-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="60895-154">запрашивает состояние с помощью этого идентификатора импорта Hello следующие:</span><span class="sxs-lookup"><span data-stu-id="60895-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="60895-155">Если задачу hello еще не завершен, hello HTTP-ответа можно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="60895-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="60895-156">Если задачу hello завершена, hello HTTP-ответа может быть несколько следующим образом:</span><span class="sxs-lookup"><span data-stu-id="60895-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="60895-157">Подключение к источнику данных \(и мультитенантность данных)</span><span class="sxs-lookup"><span data-stu-id="60895-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="60895-158">Почти все артефакты hello в pbix-файла импортируются в нашей рабочей области, hello учетные данные для источников данных, но не являются.</span><span class="sxs-lookup"><span data-stu-id="60895-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="60895-159">Таким образом, при использовании **режим DirectQuery**, hello внедренный отчет, не может отображаться неправильно.</span><span class="sxs-lookup"><span data-stu-id="60895-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="60895-160">Однако при использовании **режим импорта**, можно просмотреть отчет hello, используя существующие импортированные данные hello.</span><span class="sxs-lookup"><span data-stu-id="60895-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="60895-161">В этом случае нам необходимо задать учетные данные hello, используя следующие шаги через вызовы REST hello.</span><span class="sxs-lookup"><span data-stu-id="60895-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="60895-162">Во-первых мы должны получить источника данных шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="60895-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="60895-163">Мы знаем, что набор данных hello **идентификатор** hello ранее возвращается идентификатор.</span><span class="sxs-lookup"><span data-stu-id="60895-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="60895-164">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="60895-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="60895-165">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="60895-165">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="60895-166">С помощью hello возвращается идентификатор шлюза и идентификатор источника данных \(см. предыдущие hello **gatewayId** и **идентификатор** в hello вернул результат), hello учетные данные для этого источника данных можно изменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="60895-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="60895-167">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="60895-167">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="60895-168">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="60895-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="60895-169">В рабочей среде можно также задать hello отдельную строку подключения для каждой рабочей области, с помощью API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="60895-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="60895-170">\(т. е., можно разделить hello базы данных для каждого из клиентов.)</span><span class="sxs-lookup"><span data-stu-id="60895-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="60895-171">следующие Hello изменяется hello строка подключения источника данных через интерфейс REST.</span><span class="sxs-lookup"><span data-stu-id="60895-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="60895-172">Или можно использовать безопасность на уровне строк в Power BI Embedded, и мы можно разделить данные hello для каждого пользователя в одном отчете.</span><span class="sxs-lookup"><span data-stu-id="60895-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="60895-173">В результате мы можем подготовить отчет для каждого клиента, используя один PBIX-файл \(который описывает пользовательский интерфейс и т. д.) и разные источники данных.</span><span class="sxs-lookup"><span data-stu-id="60895-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="60895-174">Если вы используете **режим импорта** вместо **режим DirectQuery**, нет ни одной модели toorefresh способом через API-Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="60895-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="60895-175">Локальные источники данных через шлюз Power BI пока поддерживаются в Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="60895-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="60895-176">Тем не менее, будет действительно необходимо следить за hello tookeep [блоге по Power BI](https://powerbi.microsoft.com/blog/) новые возможности и предстоящие в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="60895-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="60895-177">Аутентификация и размещение (внедрение) отчетов на веб-странице</span><span class="sxs-lookup"><span data-stu-id="60895-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="60895-178">В Здравствуйте предыдущих API REST, можно использовать клавиши доступа hello **AppKey** себя в качестве заголовка авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="60895-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="60895-179">Поскольку эти вызовы могут обрабатываться на стороне сервера hello серверной части, безопасно.</span><span class="sxs-lookup"><span data-stu-id="60895-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="60895-180">Но когда мы внедрить отчет hello в наш веб-страницы, подобные сведения безопасности будет обрабатываться с помощью JavaScript \(переднего плана).</span><span class="sxs-lookup"><span data-stu-id="60895-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="60895-181">Затем значение заголовка авторизации hello должен быть защищен.</span><span class="sxs-lookup"><span data-stu-id="60895-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="60895-182">Если наш ключ доступа будет обнаружен пользователем-злоумышленником или вредоносным кодом, то злоумышленник сможет вызывать любые операции с помощью этого ключа.</span><span class="sxs-lookup"><span data-stu-id="60895-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="60895-183">Когда мы внедрение отчета hello наш веб-страницу, необходимо использовать вычисляемый токен hello вместо ключ доступа **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="60895-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="60895-184">Нашего приложения необходимо создать hello OAuth Json Web Token \(JWT) который состоит из утверждений hello и hello вычисленная цифровая подпись.</span><span class="sxs-lookup"><span data-stu-id="60895-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="60895-185">Как показано ниже, OAuth JWT — это маркер закодированной строки с разделителями-точками.</span><span class="sxs-lookup"><span data-stu-id="60895-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="60895-186">Во-первых мы необходимо подготовить hello входное значение, которое входит в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="60895-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="60895-187">Это значение является строку в кодировке URL-адреса (rfc4648) base64 hello hello, следуя json, и они разделяются точкой hello \(.) символов.</span><span class="sxs-lookup"><span data-stu-id="60895-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="60895-188">Позже вы узнаете, как tooget hello идентификатор отчета.</span><span class="sxs-lookup"><span data-stu-id="60895-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="60895-189">Если мы хотим toouse безопасности уровня строк (RLS) с Power BI Embedded, мы также необходимо указать **username** и **роли** в утверждениях hello.</span><span class="sxs-lookup"><span data-stu-id="60895-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="60895-190">Далее необходимо создать строку в кодировке base64 hello объекта HMAC \(hello подписи) с помощью алгоритма SHA256.</span><span class="sxs-lookup"><span data-stu-id="60895-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="60895-191">Входное значение со знаком — предыдущую строку hello.</span><span class="sxs-lookup"><span data-stu-id="60895-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="60895-192">И, наконец, мы необходимо объединить hello входного значения и строки подписи с помощью период \(.) символов.</span><span class="sxs-lookup"><span data-stu-id="60895-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="60895-193">Строка Hello завершено — маркер приложения hello для внедрения отчета hello.</span><span class="sxs-lookup"><span data-stu-id="60895-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="60895-194">Даже если токен приложения hello обнаружен злонамеренным пользователем, они не удается получить hello исходного ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="60895-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="60895-195">Срок действия этого маркера приложения быстро закончится.</span><span class="sxs-lookup"><span data-stu-id="60895-195">This app token will expire quickly.</span></span>

<span data-ttu-id="60895-196">Ниже приведен пример PHP для описанных шагов.</span><span class="sxs-lookup"><span data-stu-id="60895-196">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="60895-197">Наконец внедрение отчета hello в веб-страницу приветствия</span><span class="sxs-lookup"><span data-stu-id="60895-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="60895-198">Для внедрения отчета, мы получаем hello внедрить URL-адрес и отчетов **идентификатор** с помощью следующих API-интерфейса REST hello.</span><span class="sxs-lookup"><span data-stu-id="60895-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="60895-199">**HTTP-запрос**</span><span class="sxs-lookup"><span data-stu-id="60895-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="60895-200">**HTTP-ответ**</span><span class="sxs-lookup"><span data-stu-id="60895-200">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="60895-201">В наших веб-приложения с помощью предыдущего маркера приложения hello, можно внедрять hello отчета.</span><span class="sxs-lookup"><span data-stu-id="60895-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="60895-202">Если мы рассмотрим следующий пример кода hello hello бывшая части hello такой же, как в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="60895-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="60895-203">В последней части hello, в этом примере показано hello **embedUrl** \(см. предыдущий результат hello) в hello iframe и учитываются в hello iframe токен приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60895-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="60895-204">Вам потребуется tooone toochange hello отчета идентификатор значение свой собственный.</span><span class="sxs-lookup"><span data-stu-id="60895-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="60895-205">Кроме того из-за ошибки tooa в нашей системе управления содержимым, тег iframe hello в образце кода hello считывается буквально.</span><span class="sxs-lookup"><span data-stu-id="60895-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="60895-206">Удалите из тега hello текста hello сокращаться, если скопируйте и вставьте этот образец кода.</span><span class="sxs-lookup"><span data-stu-id="60895-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="60895-207">А вот и наш результат:</span><span class="sxs-lookup"><span data-stu-id="60895-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="60895-208">В настоящее время Power BI Embedded отображаются только hello отчета в hello iframe.</span><span class="sxs-lookup"><span data-stu-id="60895-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="60895-209">Но Обратите внимание на hello [блоге по Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="60895-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="60895-210">Использовать нового клиентского API, которые будут сообщите нам отправлять сведения в hello iframe, а также получить сведения будущих улучшений. Восхитительные функции!</span><span class="sxs-lookup"><span data-stu-id="60895-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="60895-211">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="60895-211">See also</span></span>
* [<span data-ttu-id="60895-212">Аутентификация и авторизация в Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="60895-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="60895-213">У вас имеются и другие вопросы?</span><span class="sxs-lookup"><span data-stu-id="60895-213">More questions?</span></span> [<span data-ttu-id="60895-214">Повторите hello сообщества Power BI</span><span class="sxs-lookup"><span data-stu-id="60895-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

