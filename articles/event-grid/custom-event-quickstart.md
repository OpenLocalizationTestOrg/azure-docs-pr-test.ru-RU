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
# <a name="create-and-route-custom-events-with-azure-event-grid"></a>Создание и перенаправление пользовательского события со службой "Сетка событий Azure"

Azure сетки событий — это служба обработки событий для облака hello. В этой статье использовать hello Azure CLI toocreate пользовательский раздел, подписка раздела toohello и активировать результат hello tooview события hello. Как правило следует отправить tooan события конечную точку, которая отвечает toohello событиях, таких как веб-перехватчик или функция Azure. Тем не менее, toosimplify данную статью, отправить hello события tooa URL, просто собирает сообщений hello. Создать этот URL-адрес можно с помощью стороннего инструмента с открытым кодом [RequestBin](https://requestb.in/).

>[!NOTE]
>**RequestBin** — средство с открытым исходным кодом, не предназначенное для использования с высокой пропускной способностью. Hello hello средство здесь используется исключительно в качестве. При отправке нескольких событий одновременно, не могут отображаться все события в средстве hello.

Когда вы закончите, вы видите, что hello данные события отправки tooan конечной точки.

![Данные событий](./media/custom-event-quickstart/request-result.png)

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этой статье требуется управлением hello последнюю версию Azure CLI (2.0.14 или более поздней версии). версия toofind hello, запустите `az --version`. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Темами событий сетки являются ресурсы Azure, которые необходимо поместить в группу ресурсов Azure. Hello группы ресурсов — это логическая коллекция, в которой Azure ресурсы развертываются и управляются.

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. 

Hello следующий пример создает группу ресурсов с именем *gridResourceGroup* в hello *westus2* расположение.

```azurecli-interactive
az group create --name gridResourceGroup --location westus2
```

## <a name="create-a-custom-topic"></a>Создание пользовательской темы

Тема содержит определяемую пользователем конечную точку, в которой можно размещать свои события. Hello пример создает раздел hello в группе ресурсов. Замените `<topic_name>` уникальным именем для вашей темы. Имя раздела Hello должно быть уникальным, так как она представлена запись DNS. Для предварительной версии hello поддерживает сетки событий **westus2** и **westcentralus** расположения.

```azurecli-interactive
az eventgrid topic create --name <topic_name> -l westus2 -g gridResourceGroup
```

## <a name="create-a-message-endpoint"></a>Создание конечной точки сообщения

Перед подпиской toohello раздела, давайте создадим hello конечную точку для hello сообщение о событии. Чем писать код toorespond toohello событий, давайте создадим конечную точку, которая собирает сообщений hello, чтобы можно было просматривать их. RequestBin является открытым исходным кодом, стороннего средства, благодаря которой вы toocreate конечной точки и представление запросов, отправленных tooit. Go слишком[RequestBin](https://requestb.in/)и нажмите кнопку **создания RequestBin**.  Скопируйте URL-адрес ячейки hello, так как необходимо при подписке toohello раздела.

## <a name="subscribe-tooa-topic"></a>Подписка раздела tooa

Подписаться tootell разделе tooa сетки событий какие события нужно tootrack. Hello следующий пример подписывает toohello разделе создается и передает hello URL-адрес из RequestBin как hello конечную точку для уведомления о событии. Замените `<event_subscription_name>` уникальное имя для вашей подписки и `<URL_from_RequestBin>` значением hello hello предыдущих разделов. Указав конечную точку при подписке, сетки событий обрабатывает hello маршрутизации конечной точки toothat события. Для `<topic_name>`, используйте значение hello, созданного ранее. 

```azurecli-interactive
az eventgrid topic event-subscription create --name <event_subscription_name> \
  --endpoint <URL_from_RequestBin> \
  -g gridResourceGroup \
  --topic-name <topic_name>
```

## <a name="send-an-event-tooyour-topic"></a>Отправить раздел tooyour события

Теперь давайте триггера toosee событие как событие сетки распределяет конечной точки tooyour сообщений hello. Во-первых давайте получить URL-адрес hello и ключ для раздела hello. Еще раз используйте имя раздела для `<topic_name>`.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

toosimplify в этой статье мы настроили образце событий данных toosend toohello раздела. Как правило приложение или служба Azure отправит hello данные события. Следующий пример Hello получает данные о событии hello:

```azurecli-interactive
body=$(eval echo "'$(curl https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json)'")
```

Если вы `echo "$body"` видно hello событий. Hello `data` элемент hello JSON является hello полезных данных события. Любое значение JSON с правильным форматом может быть в этом поле. Поле темы hello также можно дополнительно маршрутизации и фильтрации.

CURL — это служебная программа, выполняющая HTTP-запросы. В этой статье мы используем ПЕРЕЛИСТЫВАНИЕ toosend hello событие tooour раздела. 

```azurecli-interactive
curl -X POST -H "aeg-sas-key: $key" -d "$body" $endpoint
```

Появления события hello и сетки события отправляются конечной точки toohello hello сообщений, настроенных при подписке. Обзор toohello RequestBin URL-адрес, созданный ранее. Или нажмите кнопку "Обновить" в вашем открытом браузере RequestBin. Вы видите hello событий, который вы отправили. 

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

## <a name="clean-up-resources"></a>Очистка ресурсов
Если планируется toocontinue при работе с этим событием, выполните не очистить ресурсы hello, созданные в этой статье. Если вы не планируете toocontinue, используйте следующие ресурсы hello toodelete команд, созданных в данной статье hello.

```azurecli-interactive
az group delete --name gridResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы знаете, как toocreate разделы и подписки на события, Дополнительные сведения о какой сетки событий может помочь сделать:

- [An introduction to Azure Event Grid](overview.md) (Общие сведения о службе "Сетка событий Azure")
- [Monitor virtual machine changes with Azure Event Grid and Logic Apps](monitor-virtual-machine-changes-event-grid-logic-app.md) (Отслеживание изменений виртуальной машины с помощью Azure Logic Apps и службы "Сетка событий Azure")
