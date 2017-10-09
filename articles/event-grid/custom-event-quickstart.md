---
title: "aaaCustom событий для события сетки Azure | Документы Microsoft"
description: "Использовать toopublish сетки событий Azure раздела и подписки toothat событий."
services: event-grid
keywords: 
author: djrosanova
ms.author: darosa
ms.date: 08/15/2017
ms.topic: hero-article
ms.service: event-grid
ms.openlocfilehash: 5055df1c970b043cadf06978a076f7f5c83501cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-route-custom-events-with-azure-event-grid"></a><span data-ttu-id="4e331-103">Создание и перенаправление пользовательского события со службой "Сетка событий Azure"</span><span class="sxs-lookup"><span data-stu-id="4e331-103">Create and route custom events with Azure Event Grid</span></span>

<span data-ttu-id="4e331-104">Azure сетки событий — это служба обработки событий для облака hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-104">Azure Event Grid is an eventing service for hello cloud.</span></span> <span data-ttu-id="4e331-105">В этой статье использовать hello Azure CLI toocreate пользовательский раздел, подписка раздела toohello и активировать результат hello tooview события hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-105">In this article, you use hello Azure CLI toocreate a custom topic, subscribe toohello topic, and trigger hello event tooview hello result.</span></span> <span data-ttu-id="4e331-106">Как правило следует отправить tooan события конечную точку, которая отвечает toohello событиях, таких как веб-перехватчик или функция Azure.</span><span class="sxs-lookup"><span data-stu-id="4e331-106">Typically, you send events tooan endpoint that responds toohello event, such as, a webhook or Azure Function.</span></span> <span data-ttu-id="4e331-107">Тем не менее, toosimplify данную статью, отправить hello события tooa URL, просто собирает сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-107">However, toosimplify this article, you send hello events tooa URL that merely collects hello messages.</span></span> <span data-ttu-id="4e331-108">Создать этот URL-адрес можно с помощью стороннего инструмента с открытым кодом [RequestBin](https://requestb.in/).</span><span class="sxs-lookup"><span data-stu-id="4e331-108">You create this URL by using an open source, third-party tool called [RequestBin](https://requestb.in/).</span></span>

>[!NOTE]
><span data-ttu-id="4e331-109">**RequestBin** — средство с открытым исходным кодом, не предназначенное для использования с высокой пропускной способностью.</span><span class="sxs-lookup"><span data-stu-id="4e331-109">**RequestBin** is an open source tool that is not intended for high throughput usage.</span></span> <span data-ttu-id="4e331-110">Hello hello средство здесь используется исключительно в качестве.</span><span class="sxs-lookup"><span data-stu-id="4e331-110">hello use of hello tool here is purely demonstrative.</span></span> <span data-ttu-id="4e331-111">При отправке нескольких событий одновременно, не могут отображаться все события в средстве hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-111">If you push more than one event at a time, you might not see all of your events in hello tool.</span></span>

<span data-ttu-id="4e331-112">Когда вы закончите, вы видите, что hello данные события отправки tooan конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4e331-112">When you are finished, you see that hello event data has been sent tooan endpoint.</span></span>

![Данные событий](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4e331-114">Если выбрать tooinstall и использовать hello CLI локально, в этой статье требуется управлением hello последнюю версию Azure CLI (2.0.14 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="4e331-114">If you choose tooinstall and use hello CLI locally, this article requires that you are running hello latest version of Azure CLI (2.0.14 or later).</span></span> <span data-ttu-id="4e331-115">версия toofind hello, запустите `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4e331-115">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="4e331-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4e331-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="4e331-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="4e331-117">Create a resource group</span></span>

<span data-ttu-id="4e331-118">Темами событий сетки являются ресурсы Azure, которые необходимо поместить в группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="4e331-118">Event Grid topics are Azure resources, and must be placed in an Azure resource group.</span></span> <span data-ttu-id="4e331-119">Hello группы ресурсов — это логическая коллекция, в которой Azure ресурсы развертываются и управляются.</span><span class="sxs-lookup"><span data-stu-id="4e331-119">hello resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="4e331-120">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="4e331-120">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="4e331-121">Hello следующий пример создает группу ресурсов с именем *gridResourceGroup* в hello *westus2* расположение.</span><span class="sxs-lookup"><span data-stu-id="4e331-121">hello following example creates a resource group named *gridResourceGroup* in hello *westus2* location.</span></span>

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a><span data-ttu-id="4e331-122">Создание пользовательской темы</span><span class="sxs-lookup"><span data-stu-id="4e331-122">Create a custom topic</span></span>

<span data-ttu-id="4e331-123">Тема содержит определяемую пользователем конечную точку, в которой можно размещать свои события.</span><span class="sxs-lookup"><span data-stu-id="4e331-123">A topic provides a user-defined endpoint that you post your events to.</span></span> <span data-ttu-id="4e331-124">Hello пример создает раздел hello в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4e331-124">hello following example creates hello topic in your resource group.</span></span> <span data-ttu-id="4e331-125">Замените `<topic_name>` уникальным именем для вашей темы.</span><span class="sxs-lookup"><span data-stu-id="4e331-125">Replace `<topic_name>` with a unique name for your topic.</span></span> <span data-ttu-id="4e331-126">Имя раздела Hello должно быть уникальным, так как она представлена запись DNS.</span><span class="sxs-lookup"><span data-stu-id="4e331-126">hello topic name must be unique because it is represented by a DNS entry.</span></span> <span data-ttu-id="4e331-127">Для предварительной версии hello поддерживает сетки событий **westus2** и **westcentralus** расположения.</span><span class="sxs-lookup"><span data-stu-id="4e331-127">For hello preview release, Event Grid supports **westus2** and **westcentralus** locations.</span></span>

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a><span data-ttu-id="4e331-128">Создание конечной точки сообщения</span><span class="sxs-lookup"><span data-stu-id="4e331-128">Create a message endpoint</span></span>

<span data-ttu-id="4e331-129">Перед подпиской toohello раздела, давайте создадим hello конечную точку для hello сообщение о событии.</span><span class="sxs-lookup"><span data-stu-id="4e331-129">Before subscribing toohello topic, let's create hello endpoint for hello event message.</span></span> <span data-ttu-id="4e331-130">Чем писать код toorespond toohello событий, давайте создадим конечную точку, которая собирает сообщений hello, чтобы можно было просматривать их.</span><span class="sxs-lookup"><span data-stu-id="4e331-130">Rather than write code toorespond toohello event, let's create an endpoint that collects hello messages so you can view them.</span></span> <span data-ttu-id="4e331-131">RequestBin является открытым исходным кодом, стороннего средства, благодаря которой вы toocreate конечной точки и представление запросов, отправленных tooit.</span><span class="sxs-lookup"><span data-stu-id="4e331-131">RequestBin is an open source, third-party tool that enables you toocreate an endpoint, and view requests that are sent tooit.</span></span> <span data-ttu-id="4e331-132">Go слишком[RequestBin](https://requestb.in/)и нажмите кнопку **создания RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="4e331-132">Go too[RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span>  <span data-ttu-id="4e331-133">Скопируйте URL-адрес ячейки hello, так как необходимо при подписке toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="4e331-133">Copy hello bin URL, because you need it when subscribing toohello topic.</span></span>

## <a name="subscribe-tooa-topic"></a><span data-ttu-id="4e331-134">Подписка раздела tooa</span><span class="sxs-lookup"><span data-stu-id="4e331-134">Subscribe tooa topic</span></span>

<span data-ttu-id="4e331-135">Подписаться tootell разделе tooa сетки событий какие события нужно tootrack.</span><span class="sxs-lookup"><span data-stu-id="4e331-135">You subscribe tooa topic tootell Event Grid which events you want tootrack.</span></span> <span data-ttu-id="4e331-136">Hello следующий пример подписывает toohello разделе создается и передает hello URL-адрес из RequestBin как hello конечную точку для уведомления о событии.</span><span class="sxs-lookup"><span data-stu-id="4e331-136">hello following example subscribes toohello topic you created, and passes hello URL from RequestBin as hello endpoint for event notification.</span></span> <span data-ttu-id="4e331-137">Замените `<event_subscription_name>` уникальное имя для вашей подписки и `<URL_from_RequestBin>` значением hello hello предыдущих разделов.</span><span class="sxs-lookup"><span data-stu-id="4e331-137">Replace `<event_subscription_name>` with a unique name for your subscription, and `<URL_from_RequestBin>` with hello value from hello preceding section.</span></span> <span data-ttu-id="4e331-138">Указав конечную точку при подписке, сетки событий обрабатывает hello маршрутизации конечной точки toothat события.</span><span class="sxs-lookup"><span data-stu-id="4e331-138">By specifying an endpoint when subscribing, Event Grid handles hello routing of events toothat endpoint.</span></span> <span data-ttu-id="4e331-139">Для `<topic_name>`, используйте значение hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="4e331-139">For `<topic_name>`, use hello value you created earlier.</span></span> 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a><span data-ttu-id="4e331-140">Отправить раздел tooyour события</span><span class="sxs-lookup"><span data-stu-id="4e331-140">Send an event tooyour topic</span></span>

<span data-ttu-id="4e331-141">Теперь давайте триггера toosee событие как событие сетки распределяет конечной точки tooyour сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-141">Now, let's trigger an event toosee how Event Grid distributes hello message tooyour endpoint.</span></span> <span data-ttu-id="4e331-142">Во-первых давайте получить URL-адрес hello и ключ для раздела hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-142">First, let's get hello URL and key for hello topic.</span></span> <span data-ttu-id="4e331-143">Еще раз используйте имя раздела для `<topic_name>`.</span><span class="sxs-lookup"><span data-stu-id="4e331-143">Again, use your topic name for `<topic_name>`.</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

<span data-ttu-id="4e331-144">toosimplify в этой статье мы настроили образце событий данных toosend toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="4e331-144">toosimplify this article, we have set up sample event data toosend toohello topic.</span></span> <span data-ttu-id="4e331-145">Как правило приложение или служба Azure отправит hello данные события.</span><span class="sxs-lookup"><span data-stu-id="4e331-145">Typically, an application or Azure service would send hello event data.</span></span> <span data-ttu-id="4e331-146">Следующий пример Hello получает данные о событии hello:</span><span class="sxs-lookup"><span data-stu-id="4e331-146">hello following example gets hello event data:</span></span>

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

<span data-ttu-id="4e331-147">Если вы `echo "$body"` видно hello событий.</span><span class="sxs-lookup"><span data-stu-id="4e331-147">If you `echo "$body"` you can see hello full event.</span></span> <span data-ttu-id="4e331-148">Hello `data` элемент hello JSON является hello полезных данных события.</span><span class="sxs-lookup"><span data-stu-id="4e331-148">hello `data` element of hello JSON is hello payload of your event.</span></span> <span data-ttu-id="4e331-149">Любое значение JSON с правильным форматом может быть в этом поле.</span><span class="sxs-lookup"><span data-stu-id="4e331-149">Any well-formed JSON can go in this field.</span></span> <span data-ttu-id="4e331-150">Поле темы hello также можно дополнительно маршрутизации и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="4e331-150">You can also use hello subject field for advanced routing and filtering.</span></span>

<span data-ttu-id="4e331-151">CURL — это служебная программа, выполняющая HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="4e331-151">CURL is a utility that performs HTTP requests.</span></span> <span data-ttu-id="4e331-152">В этой статье мы используем ПЕРЕЛИСТЫВАНИЕ toosend hello событие tooour раздела.</span><span class="sxs-lookup"><span data-stu-id="4e331-152">In this article, we use CURL toosend hello event tooour topic.</span></span> 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

<span data-ttu-id="4e331-153">Появления события hello и сетки события отправляются конечной точки toohello hello сообщений, настроенных при подписке.</span><span class="sxs-lookup"><span data-stu-id="4e331-153">You have triggered hello event, and Event Grid sent hello message toohello endpoint you configured when subscribing.</span></span> <span data-ttu-id="4e331-154">Обзор toohello RequestBin URL-адрес, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="4e331-154">Browse toohello RequestBin URL that you created earlier.</span></span> <span data-ttu-id="4e331-155">Или нажмите кнопку "Обновить" в вашем открытом браузере RequestBin.</span><span class="sxs-lookup"><span data-stu-id="4e331-155">Or, click refresh in your open RequestBin browser.</span></span> <span data-ttu-id="4e331-156">Вы видите hello событий, который вы отправили.</span><span class="sxs-lookup"><span data-stu-id="4e331-156">You see hello event you just sent.</span></span> 

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "topic": "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/topics/{topic}"
}]
```

## <a name="clean-up-resources"></a><span data-ttu-id="4e331-157">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="4e331-157">Clean up resources</span></span>
<span data-ttu-id="4e331-158">Если планируется toocontinue при работе с этим событием, выполните не очистить ресурсы hello, созданные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4e331-158">If you plan toocontinue working with this event, do not clean up hello resources created in this article.</span></span> <span data-ttu-id="4e331-159">Если вы не планируете toocontinue, используйте следующие ресурсы hello toodelete команд, созданных в данной статье hello.</span><span class="sxs-lookup"><span data-stu-id="4e331-159">If you do not plan toocontinue, use hello following command toodelete hello resources you created in this article.</span></span>

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4e331-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e331-160">Next steps</span></span>

<span data-ttu-id="4e331-161">Теперь, когда вы знаете, как toocreate разделы и подписки на события, Дополнительные сведения о какой сетки событий может помочь сделать:</span><span class="sxs-lookup"><span data-stu-id="4e331-161">Now that you know how toocreate topics and event subscriptions, learn more about what Event Grid can help you do:</span></span>

- <span data-ttu-id="4e331-162">[An introduction to Azure Event Grid](overview.md) (Общие сведения о службе "Сетка событий Azure")</span><span class="sxs-lookup"><span data-stu-id="4e331-162">[About Event Grid](overview.md)</span></span>
- <span data-ttu-id="4e331-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Отслеживание изменений виртуальной машины с помощью Azure Logic Apps и службы "Сетка событий Azure")</span><span class="sxs-lookup"><span data-stu-id="4e331-163">[Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md)</span></span>
