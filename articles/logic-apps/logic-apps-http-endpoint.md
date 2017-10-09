---
title: "для вызова aaaCall, или вложить рабочих процессов с конечными точками HTTP - приложения логики Azure | Документы Microsoft"
description: "Настройка toocall конечные точки HTTP, триггер или вложенные рабочие процессы для логики приложений Azure"
services: logic-apps
keywords: "рабочие процессы, конечные точки HTTP"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="06612-104">Вызовы, срабатывания триггеров и создание вложенных рабочих процессов в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="06612-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="06612-105">Вы можете предоставлять доступ к синхронным конечным точкам HTTP, выступающим в качестве триггеров в приложениях логики, с помощью которых можно активировать или вызвать приложение логики через URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="06612-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="06612-106">Также вы можете создавать вложенные рабочие процессы в приложениях логики с помощью шаблона вызываемых конечных точек.</span><span class="sxs-lookup"><span data-stu-id="06612-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="06612-107">toocreate конечные точки HTTP, можно добавить эти триггеры, чтобы логика приложения могли получать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="06612-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="06612-108">Запрос</span><span class="sxs-lookup"><span data-stu-id="06612-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="06612-109">webhook API подключения;</span><span class="sxs-lookup"><span data-stu-id="06612-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="06612-110">webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="06612-111">Несмотря на то, что наши примеры использования hello **запроса** триггера, можно использовать любой из hello в списке триггеры HTTP, и все принципы применимы идентично toohello других типов триггеров.</span><span class="sxs-lookup"><span data-stu-id="06612-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="06612-112">Настройка конечной точки HTTP для приложения логики</span><span class="sxs-lookup"><span data-stu-id="06612-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="06612-113">toocreate конечную точку HTTP, добавьте триггер, который может принимать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="06612-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="06612-114">Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="06612-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="06612-115">Перейдите tooyour логику приложения и откройте конструктор логику приложения.</span><span class="sxs-lookup"><span data-stu-id="06612-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="06612-116">Добавьте триггер, который позволяет приложению логики получать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="06612-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="06612-117">Например, добавить hello **запроса** триггер tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="06612-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="06612-118">В разделе **схемы JSON тело запроса**, при необходимости можно ввести схему JSON для hello полезных данных, предполагается, что триггер tooreceive hello.</span><span class="sxs-lookup"><span data-stu-id="06612-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="06612-119">Конструктор Hello эта схема используется для создания токенов, логика приложения можно использовать tooconsume, синтаксический анализ и передачи данных из триггера hello через рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="06612-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="06612-120">Дополнительные сведения о [токенах, созданных из схем JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="06612-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="06612-121">Например введите схему hello, показанные в конструкторе hello:</span><span class="sxs-lookup"><span data-stu-id="06612-121">For this example, enter hello schema shown in hello designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Добавить действие hello запроса][1]

    > [!TIP]
    > 
    > <span data-ttu-id="06612-123">Можно создать схему для образца полезных данных JSON из средств, например [jsonschema.net](http://jsonschema.net/), или в hello **запроса** триггер, выбрав **используйте образец полезных данных toogenerate схемы**.</span><span class="sxs-lookup"><span data-stu-id="06612-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="06612-124">Введите образец полезных данных и выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="06612-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="06612-125">Например, образец полезных данных</span><span class="sxs-lookup"><span data-stu-id="06612-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="06612-126">создает эту схему:</span><span class="sxs-lookup"><span data-stu-id="06612-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="06612-127">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="06612-127">Save your logic app.</span></span> <span data-ttu-id="06612-128">В разделе **URL-адрес HTTP POST toothis**, теперь необходимо найти URL-адрес созданного обратного вызова, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="06612-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Созданный URL-адрес обратного вызова для конечной точки](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="06612-130">Этот URL-адрес содержит ключ подписи общего доступа (SAS) в параметрах запроса hello, которые используются для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="06612-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="06612-131">Можно также получить URL-адрес конечной точки HTTP hello из вашего Обзор приложений логики в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="06612-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="06612-132">В разделе **Журнал триггеров** выберите триггер:</span><span class="sxs-lookup"><span data-stu-id="06612-132">Under **Trigger History**, select your trigger:</span></span>

    ![Получение URL-адреса конечной точки HTTP на портале Azure][2]

    <span data-ttu-id="06612-134">Или hello URL-адрес можно получить, выполнив вызов:</span><span class="sxs-lookup"><span data-stu-id="06612-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="06612-135">Измените триггер hello HTTP-метод</span><span class="sxs-lookup"><span data-stu-id="06612-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="06612-136">По умолчанию hello **запроса** триггер ожидает запрос HTTP POST, но можно использовать другой метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="06612-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="06612-137">Вы можете указать только один тип метода.</span><span class="sxs-lookup"><span data-stu-id="06612-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="06612-138">Для триггера **запроса** выберите **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="06612-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="06612-139">Откройте hello **метод** списка.</span><span class="sxs-lookup"><span data-stu-id="06612-139">Open hello **Method** list.</span></span> <span data-ttu-id="06612-140">В этом примере выберите **GET**, чтобы вы могли позже проверить URL-адрес конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="06612-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="06612-141">Вы можете выбрать любой другой метод HTTP или указать пользовательский метод для своего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="06612-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Изменение метода HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="06612-143">Принятие параметров через URL-адрес конечной точки HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="06612-144">При необходимости параметры tooaccept URL-адрес конечной точки HTTP необходимо настроить код триггера относительный путь.</span><span class="sxs-lookup"><span data-stu-id="06612-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="06612-145">Для триггера **запроса** выберите **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="06612-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="06612-146">В разделе **метод**, укажите метод hello HTTP, которые должны toouse ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="06612-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="06612-147">Для этого примера выберите hello **получить** метод, если вы еще не сделали этого, благодаря чему можно протестировать URL-адрес конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="06612-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="06612-148">Когда вы указываете относительный путь для своего триггера, вы должны явно указать для триггера метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="06612-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="06612-149">В разделе **относительный путь**, укажите hello относительный путь для параметра hello, допускаемые URL-адрес, например, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="06612-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Укажите метод HTTP hello и относительный путь для параметра](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="06612-151">toouse Здравствуйте параметра, добавьте **ответ** действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="06612-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="06612-152">(Для вашего триггера выберите **Новый шаг** > **Добавить действие** > **Ответ**.)</span><span class="sxs-lookup"><span data-stu-id="06612-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="06612-153">В ваш ответ **текст**, включают hello маркер параметра hello, указанное в код триггера относительный путь.</span><span class="sxs-lookup"><span data-stu-id="06612-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="06612-154">Например, tooreturn `Hello {customerID}`, обновите ваш ответ **текст** с `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="06612-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="06612-155">Hello динамического содержимого списка должны отображаться и демонстрировать hello `customerID` маркера для вас tooselect.</span><span class="sxs-lookup"><span data-stu-id="06612-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Добавьте параметр tooresponse тело](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="06612-157">Поле **текста** должно выглядеть, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="06612-157">Your **Body** should look like this example:</span></span>

    ![Поле текста ответа с параметром](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="06612-159">Сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="06612-159">Save your logic app.</span></span> 

    <span data-ttu-id="06612-160">URL-адрес конечной точки HTTP теперь включает hello относительный путь, например:</span><span class="sxs-lookup"><span data-stu-id="06612-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="06612-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="06612-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="06612-162">tootest ваш конечная точка HTTP, копировать и вставить hello обновленный URL-адрес в другом окне браузера, но заменить `{customerID}` с `123456`, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="06612-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="06612-163">Браузер должен вывести следующий текст:</span><span class="sxs-lookup"><span data-stu-id="06612-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="06612-164">Токены, создаваемые из схем JSON для вашего приложения логики</span><span class="sxs-lookup"><span data-stu-id="06612-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="06612-165">При указании схемы JSON в вашей **запроса** триггера, hello конструктор логику приложения создает токены для свойств в этой схеме.</span><span class="sxs-lookup"><span data-stu-id="06612-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="06612-166">Затем эти токены можно использовать для передачи данных через рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="06612-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="06612-167">Например, если добавить hello `title` и `name` схемы JSON свойства tooyour, токены, становятся доступны toouse на последующих этапах рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="06612-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="06612-168">Ниже приведен полный схемы JSON hello.</span><span class="sxs-lookup"><span data-stu-id="06612-168">Here is hello complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="06612-169">Создание вложенных рабочих процессов для приложений логики</span><span class="sxs-lookup"><span data-stu-id="06612-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="06612-170">Вы можете вкладывать рабочие процессы в свое приложение логики путем добавления других приложений логики, которые могут принимать запросы.</span><span class="sxs-lookup"><span data-stu-id="06612-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="06612-171">tooinclude добавить эти логику приложения hello **приложения логики Azure - выберите рабочий процесс приложения логики** действие tooyour триггера.</span><span class="sxs-lookup"><span data-stu-id="06612-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="06612-172">Затем вы можете выбрать подходящие приложения логики.</span><span class="sxs-lookup"><span data-stu-id="06612-172">You can then select from eligible logic apps.</span></span>

![Добавление другого приложения логики](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="06612-174">Вызов или запуск приложений логики через конечные точки HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="06612-175">После создания конечной точки HTTP, вы можете активировать логику приложения с помощью `POST` полный URL-адрес метода toohello.</span><span class="sxs-lookup"><span data-stu-id="06612-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="06612-176">Приложения логики имеют встроенную поддержку конечных точек прямого доступа.</span><span class="sxs-lookup"><span data-stu-id="06612-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="06612-177">Ссылка на содержимое входящего запроса</span><span class="sxs-lookup"><span data-stu-id="06612-177">Reference content from an incoming request</span></span>

<span data-ttu-id="06612-178">Если тип содержимого hello должен `application/json`, можно указать свойства hello входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="06612-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="06612-179">В противном случае содержимое обрабатывается как единый двоичный, можно передать tooother API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="06612-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="06612-180">tooreference это содержимое внутри hello рабочего процесса, необходимо преобразовать этого содержимого.</span><span class="sxs-lookup"><span data-stu-id="06612-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="06612-181">Например, если передать `application/xml` содержимого, можно использовать `@xpath()` для извлечения XPath, или `@json()` для преобразования XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="06612-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="06612-182">Дополнительные сведения о [работе с типами содержимого](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="06612-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="06612-183">tooget hello выходные данные из входящего запроса, можно использовать hello `@triggerOutputs()` функции.</span><span class="sxs-lookup"><span data-stu-id="06612-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="06612-184">выходные данные Hello может выглядеть как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="06612-184">hello output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="06612-185">tooaccess hello `body` свойства, в частности, можно использовать hello `@triggerBody()` ярлык.</span><span class="sxs-lookup"><span data-stu-id="06612-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="06612-186">Ответ toorequests</span><span class="sxs-lookup"><span data-stu-id="06612-186">Respond toorequests</span></span>

<span data-ttu-id="06612-187">Может потребоваться toorespond toocertain запросы, начинающиеся приложения логики, возвращая содержимое toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="06612-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="06612-188">Код состояния tooconstruct hello, заголовок и текст ответа, можно использовать hello **ответ** действие.</span><span class="sxs-lookup"><span data-stu-id="06612-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="06612-189">Это действие может находиться в любом месте логики приложения, не только в конце hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="06612-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="06612-190">Если логика приложения не включает **ответ**, hello HTTP конечная точка отвечает *немедленно* с **202 принято** состояния.</span><span class="sxs-lookup"><span data-stu-id="06612-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="06612-191">Кроме того, для hello исходный запрос tooget hello ответ, все действия, необходимые для ответа hello должен быть завершен в пределах hello [предельное время ожидания запроса](./logic-apps-limits-and-config.md) только при вызове рабочего процесса hello как приложение вложенных логики.</span><span class="sxs-lookup"><span data-stu-id="06612-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="06612-192">Если ответ не выполняется в течение этого предела, hello входящий запрос времени ожидания и получает hello HTTP-ответа **408 время ожидания клиента**.</span><span class="sxs-lookup"><span data-stu-id="06612-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="06612-193">Для вложенных logic apps hello родительского логику приложения по-прежнему toowait ответа до завершения, независимо от того, сколько времени требуется.</span><span class="sxs-lookup"><span data-stu-id="06612-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="06612-194">Конструкция hello ответа</span><span class="sxs-lookup"><span data-stu-id="06612-194">Construct hello response</span></span>

<span data-ttu-id="06612-195">Можно включить несколько заголовков и содержимого в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="06612-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="06612-196">В нашем примере ответ заголовок hello указывает, что ответ hello имеет тип содержимого `application/json`.</span><span class="sxs-lookup"><span data-stu-id="06612-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="06612-197">и содержит текст hello `title` и `name`, на основе схемы JSON hello ранее обновление для hello **запроса** триггера.</span><span class="sxs-lookup"><span data-stu-id="06612-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Действие ответа HTTP][3]

<span data-ttu-id="06612-199">У ответов есть следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="06612-199">Responses have these properties:</span></span>

| <span data-ttu-id="06612-200">Свойство</span><span class="sxs-lookup"><span data-stu-id="06612-200">Property</span></span> | <span data-ttu-id="06612-201">Описание</span><span class="sxs-lookup"><span data-stu-id="06612-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06612-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="06612-202">statusCode</span></span> |<span data-ttu-id="06612-203">Указывает код состояния hello HTTP для отвечает toohello входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="06612-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="06612-204">Это может быть любой допустимый код состояния, который начинается с 2xx, 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="06612-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="06612-205">Но коды состояния 3xx не допускаются.</span><span class="sxs-lookup"><span data-stu-id="06612-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="06612-206">headers</span><span class="sxs-lookup"><span data-stu-id="06612-206">headers</span></span> |<span data-ttu-id="06612-207">Определяет любое количество заголовков tooinclude в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="06612-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="06612-208">текст</span><span class="sxs-lookup"><span data-stu-id="06612-208">body</span></span> |<span data-ttu-id="06612-209">Определяет объект текста. Это может быть строка, объект JSON и даже двоичное содержимое из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="06612-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="06612-210">Вот какие схемы JSON hello выглядит как теперь для hello **ответ** действия:</span><span class="sxs-lookup"><span data-stu-id="06612-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="06612-211">Выберите tooview hello полное JSON определение приложения логики на hello конструктор логики приложения, **кода представление**.</span><span class="sxs-lookup"><span data-stu-id="06612-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="06612-212">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="06612-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="06612-213">Вопрос. Как обеспечивается безопасность URL-адресов?</span><span class="sxs-lookup"><span data-stu-id="06612-213">Q: What about URL security?</span></span>

<span data-ttu-id="06612-214">Ответ. При создании URL-адресов обратного вызова Azure обеспечивает безопасность с помощью подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="06612-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="06612-215">Подпись передается в качестве параметра запроса и проверяется перед запуском приложения логики.</span><span class="sxs-lookup"><span data-stu-id="06612-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="06612-216">Azure создает уникальное сочетание секретный ключ для каждого приложения логики, имя триггера hello и hello операцию, выполняемую с помощью подписи hello.</span><span class="sxs-lookup"><span data-stu-id="06612-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="06612-217">Поэтому если кто-то не содержит ключ доступа toohello секретный логики приложения, не может создавать действительной подписи.</span><span class="sxs-lookup"><span data-stu-id="06612-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="06612-218">Для рабочих сред и систем безопасности настоятельно не рекомендуется вызов логику приложения непосредственно из браузера hello, так как:</span><span class="sxs-lookup"><span data-stu-id="06612-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="06612-219">в URL-адрес hello появится Hello общий ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="06612-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="06612-220">Нельзя управлять безопасного содержимого политики из-за tooshared домены среди клиентов приложения логики.</span><span class="sxs-lookup"><span data-stu-id="06612-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="06612-221">Вопрос. Могу ли я дополнительно настроить конечные точки HTTP?</span><span class="sxs-lookup"><span data-stu-id="06612-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="06612-222">Ответ. Да, конечные точки HTTP поддерживают расширенную конфигурацию через [**управление API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="06612-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="06612-223">Эта служба также обеспечивает возможность hello, для всех API, включая логику приложения управления вы tooconsistently, настроить пользовательские имена доменов, используйте дополнительные методы проверки подлинности и многое другое, например:</span><span class="sxs-lookup"><span data-stu-id="06612-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="06612-224">Измените метод запроса hello</span><span class="sxs-lookup"><span data-stu-id="06612-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="06612-225">Изменить hello сегменты URL-адреса запроса hello</span><span class="sxs-lookup"><span data-stu-id="06612-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="06612-226">Настроить домены управления API в hello [портал Azure](https://portal.azure.com/ "портал Azure")</span><span class="sxs-lookup"><span data-stu-id="06612-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="06612-227">Настройка политики toocheck для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="06612-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="06612-228">Вопрос. что изменилось, при миграции схемы hello из предварительной версии hello 1 декабря 2014 г.?</span><span class="sxs-lookup"><span data-stu-id="06612-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="06612-229">Ответ. Вот сводка об этих изменениях:</span><span class="sxs-lookup"><span data-stu-id="06612-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="06612-230">Предварительная версия от 1 декабря 2014 года</span><span class="sxs-lookup"><span data-stu-id="06612-230">December 1, 2014 preview</span></span> | <span data-ttu-id="06612-231">1 июня 2016 года</span><span class="sxs-lookup"><span data-stu-id="06612-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="06612-232">Щелкните приложение API **Прослушиватель HTTP**.</span><span class="sxs-lookup"><span data-stu-id="06612-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="06612-233">Щелкните **Ручной триггер** (приложение API не требуется).</span><span class="sxs-lookup"><span data-stu-id="06612-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="06612-234">Параметр прослушивателя HTTP*Sends response automatically*(Отправляет ответ автоматически).</span><span class="sxs-lookup"><span data-stu-id="06612-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="06612-235">Либо включить **ответ** действия или не находится в определение рабочего процесса hello</span><span class="sxs-lookup"><span data-stu-id="06612-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="06612-236">Настройка базовой проверки подлинности или OAuth</span><span class="sxs-lookup"><span data-stu-id="06612-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="06612-237">с помощью управления API</span><span class="sxs-lookup"><span data-stu-id="06612-237">via API Management</span></span> |
| <span data-ttu-id="06612-238">Настройка метода HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-238">Configure HTTP method</span></span> |<span data-ttu-id="06612-239">В разделе **Показать дополнительные параметры** выберите метод HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="06612-240">Настройка относительного пути</span><span class="sxs-lookup"><span data-stu-id="06612-240">Configure relative path</span></span> |<span data-ttu-id="06612-241">В разделе **Показать дополнительные параметры** добавьте относительный путь</span><span class="sxs-lookup"><span data-stu-id="06612-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="06612-242">Справочник по hello тела входящего запроса через`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="06612-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="06612-243">Используйте для ссылки `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="06612-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="06612-244">**Отправить ответ HTTP** действие hello прослушиватель HTTP</span><span class="sxs-lookup"><span data-stu-id="06612-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="06612-245">Нажмите кнопку **запроса tooHTTP ответ** (требуется приложение не API)</span><span class="sxs-lookup"><span data-stu-id="06612-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="06612-246">Получение справки</span><span class="sxs-lookup"><span data-stu-id="06612-246">Get help</span></span>

<span data-ttu-id="06612-247">вопросы tooask ответить на вопросы и узнайте, какие другие логику приложения Azure пользователи делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="06612-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="06612-248">toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="06612-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="06612-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06612-249">Next steps</span></span>

* [<span data-ttu-id="06612-250">Создание определений приложений логики</span><span class="sxs-lookup"><span data-stu-id="06612-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="06612-251">Обработка ошибок и исключений</span><span class="sxs-lookup"><span data-stu-id="06612-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
