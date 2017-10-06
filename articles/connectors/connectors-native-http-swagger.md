---
title: "конечные точки REST aaaCall с HTTP + Swagger соединитель для приложения логики Azure | Документы Microsoft"
description: "Подключение tooREST конечных точек из приложения логики через Swagger hello HTTP + Swagger соединителя"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="3e1da-103">Приступая к работе с hello HTTP + действие Swagger</span><span class="sxs-lookup"><span data-stu-id="3e1da-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="3e1da-104">Можно создать конечную точку REST tooany первого класса соединитель через [Swagger документа](https://swagger.io) при использовании hello HTTP + Swagger действия в рабочем процессе логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3e1da-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="3e1da-105">Кроме того, можно расширить toocall логику приложения любой конечной точки REST с эффективные возможности конструктора логики приложения.</span><span class="sxs-lookup"><span data-stu-id="3e1da-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="3e1da-106">статье toocreate логику приложения с помощью соединителей, toolearn [создайте новое приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e1da-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="3e1da-107">Использование "HTTP + Swagger" в качестве триггера или действия</span><span class="sxs-lookup"><span data-stu-id="3e1da-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="3e1da-108">Здравствуйте HTTP + Swagger рабочих триггер и действие hello таким же как hello [действия HTTP](connectors-native-http.md) , но повышения удобства работы в конструкторе логики приложения, предоставляя hello API структуру и данные, возвращаемые hello [метаданных Swagger](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="3e1da-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="3e1da-109">Здравствуйте, HTTP + Swagger соединитель также можно использовать как триггер.</span><span class="sxs-lookup"><span data-stu-id="3e1da-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="3e1da-110">Tooimplement опроса триггер, выполните шаблон опроса hello, описанное в [создать пользовательский API-интерфейсы toocall другие интерфейсы API, служб и систем из приложения логики](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="3e1da-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="3e1da-111">Дополнительные сведения о [триггерах и действиях приложения логики](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e1da-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="3e1da-112">Ниже приведен пример как toouse hello HTTP + Swagger операцию, так как действие рабочего процесса в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="3e1da-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="3e1da-113">Выберите hello **новый шаг** кнопки.</span><span class="sxs-lookup"><span data-stu-id="3e1da-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="3e1da-114">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="3e1da-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="3e1da-115">Введите в поле поиска действие hello **swagger** toolist hello HTTP + Swagger действие.</span><span class="sxs-lookup"><span data-stu-id="3e1da-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Выбор действия "HTTP + Swagger"](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="3e1da-117">Тип hello URL-адрес для документа Swagger:</span><span class="sxs-lookup"><span data-stu-id="3e1da-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="3e1da-118">toowork из hello конструктор логики приложения, hello URL-адрес должен быть конечной точкой HTTPS и включен CORS.</span><span class="sxs-lookup"><span data-stu-id="3e1da-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="3e1da-119">Если документ Swagger hello не соответствует этим требованиям, можно использовать [хранилища Azure с CORS включен](#hosting-swagger-from-storage) toostore hello документа.</span><span class="sxs-lookup"><span data-stu-id="3e1da-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="3e1da-120">Нажмите кнопку **Далее** tooread и отрисовки из hello Swagger документа.</span><span class="sxs-lookup"><span data-stu-id="3e1da-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="3e1da-121">Добавьте параметры, необходимые для вызова hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e1da-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Выполнение действия HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="3e1da-123">toosave и опубликовать приложение логики, нажмите кнопку **Сохранить** на панели инструментов конструктора.</span><span class="sxs-lookup"><span data-stu-id="3e1da-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="3e1da-124">Размещение Swagger из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3e1da-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="3e1da-125">Может потребоваться tooreference Swagger документа, не размещенного или, не соответствует требованиям безопасности и независимо от источника hello, для конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="3e1da-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="3e1da-126">tooresolve эту проблему, можно хранить hello Swagger документа в хранилище Azure и включить CORS tooreference hello документа.</span><span class="sxs-lookup"><span data-stu-id="3e1da-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="3e1da-127">Ниже приведены шаги toocreate hello, настройте и хранения Swagger документы в хранилище Azure:</span><span class="sxs-lookup"><span data-stu-id="3e1da-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="3e1da-128">[Создайте учетную запись Azure с хранилищем BLOB-объектов Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3e1da-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="3e1da-129">tooperform это действие, задание разрешений слишком**общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="3e1da-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="3e1da-130">Включите CORS hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3e1da-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="3e1da-131">Этот параметр tooautomatically, можно использовать [этот сценарий PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="3e1da-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="3e1da-132">Передача большого двоичного объекта файла Swagger toohello hello.</span><span class="sxs-lookup"><span data-stu-id="3e1da-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="3e1da-133">Этот этап можно выполнить из hello [портал Azure](https://portal.azure.com) или из такого средства, как [обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="3e1da-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="3e1da-134">Ссылаться на документ toohello ссылку HTTPS в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1da-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="3e1da-135">ссылка Hello использует данный формат:</span><span class="sxs-lookup"><span data-stu-id="3e1da-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="3e1da-136">Технические сведения</span><span class="sxs-lookup"><span data-stu-id="3e1da-136">Technical details</span></span>
<span data-ttu-id="3e1da-137">Ниже приведены сведения hello для hello триггеров и действий, это HTTP + Swagger поддерживает соединитель.</span><span class="sxs-lookup"><span data-stu-id="3e1da-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="3e1da-138">Триггеры "HTTP + Swagger"</span><span class="sxs-lookup"><span data-stu-id="3e1da-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="3e1da-139">Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="3e1da-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3e1da-140">Дополнительные сведения о триггерах см. здесь.</span><span class="sxs-lookup"><span data-stu-id="3e1da-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="3e1da-141">Здравствуйте HTTP + Swagger соединитель имеет один триггер.</span><span class="sxs-lookup"><span data-stu-id="3e1da-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="3e1da-142">Триггер</span><span class="sxs-lookup"><span data-stu-id="3e1da-142">Trigger</span></span> | <span data-ttu-id="3e1da-143">Описание</span><span class="sxs-lookup"><span data-stu-id="3e1da-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e1da-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3e1da-144">HTTP + Swagger</span></span> |<span data-ttu-id="3e1da-145">Сделать вызов HTTP и возвращает содержимое ответа hello</span><span class="sxs-lookup"><span data-stu-id="3e1da-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="3e1da-146">Действия "HTTP + Swagger"</span><span class="sxs-lookup"><span data-stu-id="3e1da-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="3e1da-147">Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="3e1da-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3e1da-148">Дополнительные сведения о действиях см. здесь.</span><span class="sxs-lookup"><span data-stu-id="3e1da-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="3e1da-149">Здравствуйте HTTP + Swagger соединитель имеет единственным возможным действием.</span><span class="sxs-lookup"><span data-stu-id="3e1da-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="3e1da-150">Действие</span><span class="sxs-lookup"><span data-stu-id="3e1da-150">Action</span></span> | <span data-ttu-id="3e1da-151">Описание</span><span class="sxs-lookup"><span data-stu-id="3e1da-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e1da-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3e1da-152">HTTP + Swagger</span></span> |<span data-ttu-id="3e1da-153">Сделать вызов HTTP и возвращает содержимое ответа hello</span><span class="sxs-lookup"><span data-stu-id="3e1da-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="3e1da-154">Сведения о действиях</span><span class="sxs-lookup"><span data-stu-id="3e1da-154">Action details</span></span>
<span data-ttu-id="3e1da-155">Здравствуйте HTTP + Swagger соединитель поставляется с единственным возможным действием.</span><span class="sxs-lookup"><span data-stu-id="3e1da-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="3e1da-156">Ниже приведены сведения о каждом из действия hello, обязательные и необязательные поля ввода и соответствующие сведения о выходных данных, связанных с их использованием hello.</span><span class="sxs-lookup"><span data-stu-id="3e1da-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="3e1da-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3e1da-157">HTTP + Swagger</span></span>
<span data-ttu-id="3e1da-158">Выполните исходящий HTTP-запрос, используя метаданные Swagger.</span><span class="sxs-lookup"><span data-stu-id="3e1da-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="3e1da-159">Звездочка (*) означает, что поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="3e1da-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="3e1da-160">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="3e1da-160">Display name</span></span> | <span data-ttu-id="3e1da-161">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="3e1da-161">Property name</span></span> | <span data-ttu-id="3e1da-162">Описание</span><span class="sxs-lookup"><span data-stu-id="3e1da-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e1da-163">Метод*</span><span class="sxs-lookup"><span data-stu-id="3e1da-163">Method*</span></span> |<span data-ttu-id="3e1da-164">метод</span><span class="sxs-lookup"><span data-stu-id="3e1da-164">method</span></span> |<span data-ttu-id="3e1da-165">Toouse команд HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e1da-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="3e1da-166">URI*</span><span class="sxs-lookup"><span data-stu-id="3e1da-166">URI*</span></span> |<span data-ttu-id="3e1da-167">uri</span><span class="sxs-lookup"><span data-stu-id="3e1da-167">uri</span></span> |<span data-ttu-id="3e1da-168">URI для hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="3e1da-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="3e1da-169">Заголовки</span><span class="sxs-lookup"><span data-stu-id="3e1da-169">Headers</span></span> |<span data-ttu-id="3e1da-170">headers</span><span class="sxs-lookup"><span data-stu-id="3e1da-170">headers</span></span> |<span data-ttu-id="3e1da-171">Объект JSON tooinclude заголовков HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e1da-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="3e1da-172">Текст</span><span class="sxs-lookup"><span data-stu-id="3e1da-172">Body</span></span> |<span data-ttu-id="3e1da-173">текст</span><span class="sxs-lookup"><span data-stu-id="3e1da-173">body</span></span> |<span data-ttu-id="3e1da-174">Здравствуйте, HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="3e1da-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="3e1da-175">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="3e1da-175">Authentication</span></span> |<span data-ttu-id="3e1da-176">authentication</span><span class="sxs-lookup"><span data-stu-id="3e1da-176">authentication</span></span> |<span data-ttu-id="3e1da-177">Toouse проверки подлинности для запроса.</span><span class="sxs-lookup"><span data-stu-id="3e1da-177">Authentication toouse for request.</span></span> <span data-ttu-id="3e1da-178">Дополнительные сведения см. в разделе hello [соединителя HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="3e1da-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="3e1da-179">**Сведения о выходных данных**</span><span class="sxs-lookup"><span data-stu-id="3e1da-179">**Output details**</span></span>

<span data-ttu-id="3e1da-180">Ответ HTTP</span><span class="sxs-lookup"><span data-stu-id="3e1da-180">HTTP response</span></span>

| <span data-ttu-id="3e1da-181">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="3e1da-181">Property Name</span></span> | <span data-ttu-id="3e1da-182">Тип данных</span><span class="sxs-lookup"><span data-stu-id="3e1da-182">Data type</span></span> | <span data-ttu-id="3e1da-183">Описание</span><span class="sxs-lookup"><span data-stu-id="3e1da-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e1da-184">Заголовки</span><span class="sxs-lookup"><span data-stu-id="3e1da-184">Headers</span></span> |<span data-ttu-id="3e1da-185">object</span><span class="sxs-lookup"><span data-stu-id="3e1da-185">object</span></span> |<span data-ttu-id="3e1da-186">Заголовки ответов</span><span class="sxs-lookup"><span data-stu-id="3e1da-186">Response headers</span></span> |
| <span data-ttu-id="3e1da-187">Текст</span><span class="sxs-lookup"><span data-stu-id="3e1da-187">Body</span></span> |<span data-ttu-id="3e1da-188">object</span><span class="sxs-lookup"><span data-stu-id="3e1da-188">object</span></span> |<span data-ttu-id="3e1da-189">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="3e1da-189">Response object</span></span> |
| <span data-ttu-id="3e1da-190">Код состояния</span><span class="sxs-lookup"><span data-stu-id="3e1da-190">Status Code</span></span> |<span data-ttu-id="3e1da-191">int</span><span class="sxs-lookup"><span data-stu-id="3e1da-191">int</span></span> |<span data-ttu-id="3e1da-192">HTTP status code (Код состояния HTTP)</span><span class="sxs-lookup"><span data-stu-id="3e1da-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="3e1da-193">Ответы HTTP</span><span class="sxs-lookup"><span data-stu-id="3e1da-193">HTTP responses</span></span>
<span data-ttu-id="3e1da-194">При выполнении действия toovarious вызовов, можно получить определенные ответы.</span><span class="sxs-lookup"><span data-stu-id="3e1da-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="3e1da-195">В таблице ниже приведены соответствующие ответы и описания.</span><span class="sxs-lookup"><span data-stu-id="3e1da-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="3e1da-196">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="3e1da-196">Name</span></span> | <span data-ttu-id="3e1da-197">Описание</span><span class="sxs-lookup"><span data-stu-id="3e1da-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e1da-198">200</span><span class="sxs-lookup"><span data-stu-id="3e1da-198">200</span></span> |<span data-ttu-id="3e1da-199">ОК</span><span class="sxs-lookup"><span data-stu-id="3e1da-199">OK</span></span> |
| <span data-ttu-id="3e1da-200">202</span><span class="sxs-lookup"><span data-stu-id="3e1da-200">202</span></span> |<span data-ttu-id="3e1da-201">Принято</span><span class="sxs-lookup"><span data-stu-id="3e1da-201">Accepted</span></span> |
| <span data-ttu-id="3e1da-202">400</span><span class="sxs-lookup"><span data-stu-id="3e1da-202">400</span></span> |<span data-ttu-id="3e1da-203">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="3e1da-203">Bad request</span></span> |
| <span data-ttu-id="3e1da-204">401</span><span class="sxs-lookup"><span data-stu-id="3e1da-204">401</span></span> |<span data-ttu-id="3e1da-205">Не авторизовано</span><span class="sxs-lookup"><span data-stu-id="3e1da-205">Unauthorized</span></span> |
| <span data-ttu-id="3e1da-206">403</span><span class="sxs-lookup"><span data-stu-id="3e1da-206">403</span></span> |<span data-ttu-id="3e1da-207">Запрещено</span><span class="sxs-lookup"><span data-stu-id="3e1da-207">Forbidden</span></span> |
| <span data-ttu-id="3e1da-208">404</span><span class="sxs-lookup"><span data-stu-id="3e1da-208">404</span></span> |<span data-ttu-id="3e1da-209">Не найдено</span><span class="sxs-lookup"><span data-stu-id="3e1da-209">Not Found</span></span> |
| <span data-ttu-id="3e1da-210">500</span><span class="sxs-lookup"><span data-stu-id="3e1da-210">500</span></span> |<span data-ttu-id="3e1da-211">Внутренняя ошибка сервера.</span><span class="sxs-lookup"><span data-stu-id="3e1da-211">Internal server error.</span></span> <span data-ttu-id="3e1da-212">Произошла неизвестная ошибка.</span><span class="sxs-lookup"><span data-stu-id="3e1da-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="3e1da-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e1da-213">Next steps</span></span>

* [<span data-ttu-id="3e1da-214">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="3e1da-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="3e1da-215">Список соединителей</span><span class="sxs-lookup"><span data-stu-id="3e1da-215">Find other connectors</span></span>](apis-list.md)