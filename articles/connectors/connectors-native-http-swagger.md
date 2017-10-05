---
title: "Вызов конечных точек REST с помощью соединителя HTTP + Swagger для Azure Logic Apps | Документация Майкрософт"
description: "Выполните подключение к конечным точкам REST из приложений логики в Swagger с помощью соединителя HTTP + Swagger"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="1ec06-103">Приступая к работе с действием "HTTP + Swagger"</span><span class="sxs-lookup"><span data-stu-id="1ec06-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="1ec06-104">Выполнив действие HTTP + Swagger в рабочем процессе приложения логики, можно создать первоклассный соединитель для любой конечной точки REST с применением [документа Swagger](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="1ec06-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="1ec06-105">Первоклассный конструктор приложений логики позволяет расширить функциональность приложения логики, обеспечив возможность вызова любой конечной точки REST.</span><span class="sxs-lookup"><span data-stu-id="1ec06-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="1ec06-106">Сведения о создании приложения логики с помощью соединителей см. в [этой статье](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ec06-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="1ec06-107">Использование "HTTP + Swagger" в качестве триггера или действия</span><span class="sxs-lookup"><span data-stu-id="1ec06-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="1ec06-108">Триггер и действие HTTP + Swagger выполняют те же функции, что и [действие HTTP](connectors-native-http.md), но обеспечивают более широкие возможности при работе с конструктором приложений логики, предоставляя структуру и выходные данные API из [метаданных Swagger](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="1ec06-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="1ec06-109">Соединитель HTTP + Swagger также можно использовать в качестве триггера.</span><span class="sxs-lookup"><span data-stu-id="1ec06-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="1ec06-110">Для внедрения опрашивающего триггера используйте шаблон опроса, описанный в статье [Создание пользовательского API для приложений логики](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="1ec06-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="1ec06-111">Дополнительные сведения о [триггерах и действиях приложения логики](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ec06-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="1ec06-112">Ниже приведен пример использования операции "HTTP + Swagger" в качестве действия в рабочем процессе приложения логики.</span><span class="sxs-lookup"><span data-stu-id="1ec06-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="1ec06-113">Нажмите кнопку **Новый шаг** .</span><span class="sxs-lookup"><span data-stu-id="1ec06-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="1ec06-114">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="1ec06-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="1ec06-115">В поле поиска действий введите **swagger** , чтобы в списке отобразилось действие "HTTP + Swagger".</span><span class="sxs-lookup"><span data-stu-id="1ec06-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Выбор действия "HTTP + Swagger"](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="1ec06-117">Введите URL-адрес документа Swagger.</span><span class="sxs-lookup"><span data-stu-id="1ec06-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="1ec06-118">При использовании конструктора приложений логики URL-адресом должна быть конечная точка HTTPS с включенной поддержкой CORS.</span><span class="sxs-lookup"><span data-stu-id="1ec06-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="1ec06-119">Если для документа Swagger не выполняется данное требование, то для его хранения можно воспользоваться [службой хранилища Azure с включенной поддержкой CORS](#hosting-swagger-from-storage) .</span><span class="sxs-lookup"><span data-stu-id="1ec06-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="1ec06-120">Для чтения и обработки из документа Swagger нажмите кнопку **Далее** .</span><span class="sxs-lookup"><span data-stu-id="1ec06-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="1ec06-121">Добавьте параметры, необходимые для вызова HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ec06-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Выполнение действия HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="1ec06-123">Чтобы сохранить и опубликовать свое приложение логики, на панели инструментов конструктора нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1ec06-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="1ec06-124">Размещение Swagger из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="1ec06-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="1ec06-125">Вам может потребоваться задать ссылку на документ Swagger, который еще не размещен или не соответствует требованиям безопасности и CORS, из-за чего он не может использоваться в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="1ec06-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="1ec06-126">Для решения этой проблемы можно сохранить документ Swagger в службе хранилища Azure и включить поддержку CORS, что позволит задать ссылку на документ.</span><span class="sxs-lookup"><span data-stu-id="1ec06-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="1ec06-127">Выполните приведенные ниже шаги, чтобы создать, настроить и сохранить документы Swagger в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec06-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="1ec06-128">[Создайте учетную запись Azure с хранилищем BLOB-объектов Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1ec06-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="1ec06-129">Чтобы выполнить этот шаг, установите для разрешений значение **Public Access** (Общий доступ).</span><span class="sxs-lookup"><span data-stu-id="1ec06-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="1ec06-130">Включите поддержку CORS для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="1ec06-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="1ec06-131">Для автоматической настройки данного параметра можно использовать [этот сценарий PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="1ec06-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="1ec06-132">Передайте файл Swagger в большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="1ec06-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="1ec06-133">Это можно сделать на [портале Azure](https://portal.azure.com) или с помощью инструмента, такого как [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1ec06-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="1ec06-134">Задайте ссылку HTTPS на документ в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec06-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="1ec06-135">В связи с этим используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1ec06-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="1ec06-136">Технические сведения</span><span class="sxs-lookup"><span data-stu-id="1ec06-136">Technical details</span></span>
<span data-ttu-id="1ec06-137">Ниже приведены подробные сведения о триггерах и действиях, поддерживаемых соединителем "HTTP + Swagger".</span><span class="sxs-lookup"><span data-stu-id="1ec06-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="1ec06-138">Триггеры "HTTP + Swagger"</span><span class="sxs-lookup"><span data-stu-id="1ec06-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="1ec06-139">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="1ec06-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="1ec06-140">Дополнительные сведения о триггерах см. здесь.</span><span class="sxs-lookup"><span data-stu-id="1ec06-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="1ec06-141">У соединителя "HTTP + Swagger" один триггер.</span><span class="sxs-lookup"><span data-stu-id="1ec06-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="1ec06-142">Триггер</span><span class="sxs-lookup"><span data-stu-id="1ec06-142">Trigger</span></span> | <span data-ttu-id="1ec06-143">Описание</span><span class="sxs-lookup"><span data-stu-id="1ec06-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ec06-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="1ec06-144">HTTP + Swagger</span></span> |<span data-ttu-id="1ec06-145">Вызов HTTP и возврат содержимого ответа</span><span class="sxs-lookup"><span data-stu-id="1ec06-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="1ec06-146">Действия "HTTP + Swagger"</span><span class="sxs-lookup"><span data-stu-id="1ec06-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="1ec06-147">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="1ec06-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="1ec06-148">Дополнительные сведения о действиях см. здесь.</span><span class="sxs-lookup"><span data-stu-id="1ec06-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="1ec06-149">У соединителя "HTTP + Swagger" одно возможное действие.</span><span class="sxs-lookup"><span data-stu-id="1ec06-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="1ec06-150">Действие</span><span class="sxs-lookup"><span data-stu-id="1ec06-150">Action</span></span> | <span data-ttu-id="1ec06-151">Описание</span><span class="sxs-lookup"><span data-stu-id="1ec06-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ec06-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="1ec06-152">HTTP + Swagger</span></span> |<span data-ttu-id="1ec06-153">Вызов HTTP и возврат содержимого ответа</span><span class="sxs-lookup"><span data-stu-id="1ec06-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="1ec06-154">Сведения о действиях</span><span class="sxs-lookup"><span data-stu-id="1ec06-154">Action details</span></span>
<span data-ttu-id="1ec06-155">У соединителя "HTTP + Swagger" одно возможное действие.</span><span class="sxs-lookup"><span data-stu-id="1ec06-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="1ec06-156">Ниже приведены сведения о всех действиях, их обязательных и необязательных полях ввода, а также соответствующие выходные данные, связанные с их использованием.</span><span class="sxs-lookup"><span data-stu-id="1ec06-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="1ec06-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="1ec06-157">HTTP + Swagger</span></span>
<span data-ttu-id="1ec06-158">Выполните исходящий HTTP-запрос, используя метаданные Swagger.</span><span class="sxs-lookup"><span data-stu-id="1ec06-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="1ec06-159">Звездочка (*) означает, что поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="1ec06-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="1ec06-160">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="1ec06-160">Display name</span></span> | <span data-ttu-id="1ec06-161">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1ec06-161">Property name</span></span> | <span data-ttu-id="1ec06-162">Описание</span><span class="sxs-lookup"><span data-stu-id="1ec06-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ec06-163">Метод*</span><span class="sxs-lookup"><span data-stu-id="1ec06-163">Method*</span></span> |<span data-ttu-id="1ec06-164">метод</span><span class="sxs-lookup"><span data-stu-id="1ec06-164">method</span></span> |<span data-ttu-id="1ec06-165">HTTP-команда для использования.</span><span class="sxs-lookup"><span data-stu-id="1ec06-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="1ec06-166">URI*</span><span class="sxs-lookup"><span data-stu-id="1ec06-166">URI*</span></span> |<span data-ttu-id="1ec06-167">uri</span><span class="sxs-lookup"><span data-stu-id="1ec06-167">uri</span></span> |<span data-ttu-id="1ec06-168">URI HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1ec06-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="1ec06-169">Заголовки</span><span class="sxs-lookup"><span data-stu-id="1ec06-169">Headers</span></span> |<span data-ttu-id="1ec06-170">headers</span><span class="sxs-lookup"><span data-stu-id="1ec06-170">headers</span></span> |<span data-ttu-id="1ec06-171">Объект JSON заголовков HTTP, который необходимо включить.</span><span class="sxs-lookup"><span data-stu-id="1ec06-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="1ec06-172">Текст</span><span class="sxs-lookup"><span data-stu-id="1ec06-172">Body</span></span> |<span data-ttu-id="1ec06-173">текст</span><span class="sxs-lookup"><span data-stu-id="1ec06-173">body</span></span> |<span data-ttu-id="1ec06-174">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="1ec06-174">The HTTP request body.</span></span> |
| <span data-ttu-id="1ec06-175">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="1ec06-175">Authentication</span></span> |<span data-ttu-id="1ec06-176">authentication</span><span class="sxs-lookup"><span data-stu-id="1ec06-176">authentication</span></span> |<span data-ttu-id="1ec06-177">Аутентификация, используемая для запроса.</span><span class="sxs-lookup"><span data-stu-id="1ec06-177">Authentication to use for request.</span></span> <span data-ttu-id="1ec06-178">Дополнительные сведения см. в статье о [соединителе HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="1ec06-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="1ec06-179">**Сведения о выходных данных**</span><span class="sxs-lookup"><span data-stu-id="1ec06-179">**Output details**</span></span>

<span data-ttu-id="1ec06-180">Ответ HTTP</span><span class="sxs-lookup"><span data-stu-id="1ec06-180">HTTP response</span></span>

| <span data-ttu-id="1ec06-181">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1ec06-181">Property Name</span></span> | <span data-ttu-id="1ec06-182">Тип данных</span><span class="sxs-lookup"><span data-stu-id="1ec06-182">Data type</span></span> | <span data-ttu-id="1ec06-183">Описание</span><span class="sxs-lookup"><span data-stu-id="1ec06-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ec06-184">Заголовки</span><span class="sxs-lookup"><span data-stu-id="1ec06-184">Headers</span></span> |<span data-ttu-id="1ec06-185">object</span><span class="sxs-lookup"><span data-stu-id="1ec06-185">object</span></span> |<span data-ttu-id="1ec06-186">Заголовки ответов</span><span class="sxs-lookup"><span data-stu-id="1ec06-186">Response headers</span></span> |
| <span data-ttu-id="1ec06-187">Текст</span><span class="sxs-lookup"><span data-stu-id="1ec06-187">Body</span></span> |<span data-ttu-id="1ec06-188">object</span><span class="sxs-lookup"><span data-stu-id="1ec06-188">object</span></span> |<span data-ttu-id="1ec06-189">Объект ответа</span><span class="sxs-lookup"><span data-stu-id="1ec06-189">Response object</span></span> |
| <span data-ttu-id="1ec06-190">Код состояния</span><span class="sxs-lookup"><span data-stu-id="1ec06-190">Status Code</span></span> |<span data-ttu-id="1ec06-191">int</span><span class="sxs-lookup"><span data-stu-id="1ec06-191">int</span></span> |<span data-ttu-id="1ec06-192">HTTP status code (Код состояния HTTP)</span><span class="sxs-lookup"><span data-stu-id="1ec06-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="1ec06-193">Ответы HTTP</span><span class="sxs-lookup"><span data-stu-id="1ec06-193">HTTP responses</span></span>
<span data-ttu-id="1ec06-194">В результате вызова различных действий могут возвращаться определенные ответы.</span><span class="sxs-lookup"><span data-stu-id="1ec06-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="1ec06-195">В таблице ниже приведены соответствующие ответы и описания.</span><span class="sxs-lookup"><span data-stu-id="1ec06-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="1ec06-196">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="1ec06-196">Name</span></span> | <span data-ttu-id="1ec06-197">Описание</span><span class="sxs-lookup"><span data-stu-id="1ec06-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ec06-198">200</span><span class="sxs-lookup"><span data-stu-id="1ec06-198">200</span></span> |<span data-ttu-id="1ec06-199">ОК</span><span class="sxs-lookup"><span data-stu-id="1ec06-199">OK</span></span> |
| <span data-ttu-id="1ec06-200">202</span><span class="sxs-lookup"><span data-stu-id="1ec06-200">202</span></span> |<span data-ttu-id="1ec06-201">Принято</span><span class="sxs-lookup"><span data-stu-id="1ec06-201">Accepted</span></span> |
| <span data-ttu-id="1ec06-202">400</span><span class="sxs-lookup"><span data-stu-id="1ec06-202">400</span></span> |<span data-ttu-id="1ec06-203">Недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="1ec06-203">Bad request</span></span> |
| <span data-ttu-id="1ec06-204">401</span><span class="sxs-lookup"><span data-stu-id="1ec06-204">401</span></span> |<span data-ttu-id="1ec06-205">Не авторизовано</span><span class="sxs-lookup"><span data-stu-id="1ec06-205">Unauthorized</span></span> |
| <span data-ttu-id="1ec06-206">403</span><span class="sxs-lookup"><span data-stu-id="1ec06-206">403</span></span> |<span data-ttu-id="1ec06-207">Запрещено</span><span class="sxs-lookup"><span data-stu-id="1ec06-207">Forbidden</span></span> |
| <span data-ttu-id="1ec06-208">404</span><span class="sxs-lookup"><span data-stu-id="1ec06-208">404</span></span> |<span data-ttu-id="1ec06-209">Не найдено</span><span class="sxs-lookup"><span data-stu-id="1ec06-209">Not Found</span></span> |
| <span data-ttu-id="1ec06-210">500</span><span class="sxs-lookup"><span data-stu-id="1ec06-210">500</span></span> |<span data-ttu-id="1ec06-211">Внутренняя ошибка сервера.</span><span class="sxs-lookup"><span data-stu-id="1ec06-211">Internal server error.</span></span> <span data-ttu-id="1ec06-212">Произошла неизвестная ошибка.</span><span class="sxs-lookup"><span data-stu-id="1ec06-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="1ec06-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ec06-213">Next steps</span></span>

* [<span data-ttu-id="1ec06-214">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="1ec06-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="1ec06-215">Список соединителей</span><span class="sxs-lookup"><span data-stu-id="1ec06-215">Find other connectors</span></span>](apis-list.md)