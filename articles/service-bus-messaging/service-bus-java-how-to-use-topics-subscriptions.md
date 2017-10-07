---
title: "разделы шины обслуживания Azure toouse aaaHow с Java | Документы Microsoft"
description: "Использование разделов и подписок служебной шины в Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="5a305-103">Как toouse Service Bus разделов и подписок с помощью Java</span><span class="sxs-lookup"><span data-stu-id="5a305-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="5a305-104">В этом руководстве описаны как toouse Service Bus разделы и подписки.</span><span class="sxs-lookup"><span data-stu-id="5a305-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="5a305-105">Hello примеры написаны на Java и использовать hello [пакет Azure SDK для Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5a305-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="5a305-106">Hello сценарии включают **создания разделов и подписок**, **создание фильтров подписок**, **отправки темы о сообщениях tooa**, **получения сообщения из подписки**, и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="5a305-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="5a305-107">Что такое разделы и подписки служебной шины?</span><span class="sxs-lookup"><span data-stu-id="5a305-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="5a305-108">Разделы и подписки служебной шины поддерживают модель обмена сообщениями " *публикация и подписка* ".</span><span class="sxs-lookup"><span data-stu-id="5a305-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="5a305-109">При использовании разделов и подписок компоненты распределенного приложения не взаимодействуют между собой напрямую, а обмениваются сообщениями через раздел, который выступает в качестве посредника.</span><span class="sxs-lookup"><span data-stu-id="5a305-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="5a305-111">В отличие от очередей служебной шины, где каждое сообщение обрабатывается одним потребителем, разделы и подписки предоставляют вид связи одного со многими с помощью шаблона публикации/подписки.</span><span class="sxs-lookup"><span data-stu-id="5a305-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="5a305-112">Можно зарегистрировать несколько подписок tooa раздела.</span><span class="sxs-lookup"><span data-stu-id="5a305-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="5a305-113">Когда сообщение отправляется раздел tooa, он становятся доступны tooeach подписки toohandle или процесс независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="5a305-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="5a305-114">Tooa подписка раздела напоминает виртуальную очередь, которая получает копии отправленных toohello раздел сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="5a305-115">При необходимости можно зарегистрировать правила фильтрации для раздела по подпискам, позволяющий toofilter или ограничить какие tooa темы о сообщениях, полученных какие подписок раздела.</span><span class="sxs-lookup"><span data-stu-id="5a305-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="5a305-116">Подписки и темы Service Bus позволяют tooscale tooprocess очень большое количество сообщений очень большом количестве пользователей и приложений.</span><span class="sxs-lookup"><span data-stu-id="5a305-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="5a305-117">Создание пространства имен службы</span><span class="sxs-lookup"><span data-stu-id="5a305-117">Create a service namespace</span></span>
<span data-ttu-id="5a305-118">toobegin с помощью подписки и темы Service Bus в Azure, необходимо сначала создать пространство имен, которое предоставляет контейнером для адресации ресурсов служебной шины в приложении.</span><span class="sxs-lookup"><span data-stu-id="5a305-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="5a305-119">toocreate пространство имен:</span><span class="sxs-lookup"><span data-stu-id="5a305-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5a305-120">Настройка вашего приложения toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="5a305-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5a305-121">Убедитесь, что вы установили hello [пакет Azure SDK для Java] [ Azure SDK for Java] перед построением в этом примере.</span><span class="sxs-lookup"><span data-stu-id="5a305-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="5a305-122">Если вы используете Eclipse, вы можете установить hello [средств Azure для Eclipse] [ Azure Toolkit for Eclipse] , включающего hello Azure SDK для Java.</span><span class="sxs-lookup"><span data-stu-id="5a305-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="5a305-123">Затем можно добавить hello **библиотеки Microsoft Azure для Java** tooyour проекта:</span><span class="sxs-lookup"><span data-stu-id="5a305-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="5a305-124">Добавьте следующее hello `import` вверху файла Java hello toohello инструкции:</span><span class="sxs-lookup"><span data-stu-id="5a305-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="5a305-125">Добавьте hello библиотек Azure для Java tooyour путь сборки и включите его в сборку развертывания проекта.</span><span class="sxs-lookup"><span data-stu-id="5a305-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="5a305-126">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="5a305-126">Create a topic</span></span>
<span data-ttu-id="5a305-127">Операции управления для разделов служебной шины можно выполнять с помощью класса **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="5a305-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="5a305-128">Объект **ServiceBusContract** объект создан с соответствующей конфигурации, инкапсулирующий маркер SAS toomanage разрешения и hello **ServiceBusContract** класс является единственной точкой hello связи с Azure.</span><span class="sxs-lookup"><span data-stu-id="5a305-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="5a305-129">Hello **ServiceBusService** класс предоставляет методы toocreate, перечислять и удалять разделы.</span><span class="sxs-lookup"><span data-stu-id="5a305-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="5a305-130">Следующий пример показывает как Hello **ServiceBusService** объект можно использовать toocreate раздел с именем `TestTopic`, с именем пространства имен `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="5a305-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="5a305-131">Существуют методы на **TopicInfo** , позволяющие свойства раздела hello задаваемый (например: tooset hello по умолчанию срок жизни (TTL) значение toobe применения toomessages отправлено toohello раздела).</span><span class="sxs-lookup"><span data-stu-id="5a305-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="5a305-132">Hello следующем примере показано как toocreate раздел с именем `TestTopic` с максимальным размером 5 ГБ:</span><span class="sxs-lookup"><span data-stu-id="5a305-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="5a305-133">Обратите внимание, что можно использовать hello **listTopics** метод **ServiceBusContract** объектов toocheck, если раздел с указанным именем уже существует в пространстве имен службы.</span><span class="sxs-lookup"><span data-stu-id="5a305-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="5a305-134">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="5a305-134">Create subscriptions</span></span>
<span data-ttu-id="5a305-135">Tootopics подписки также создаются с hello **ServiceBusService** класса.</span><span class="sxs-lookup"><span data-stu-id="5a305-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="5a305-136">Подписки представляют собой именованные и может иметь дополнительный фильтр, ограничивающий hello набор сообщений, передаваемых toohello в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="5a305-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="5a305-137">Создайте подписку с фильтром (MatchAll) по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="5a305-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="5a305-138">Hello **MatchAll** фильтром является фильтр по умолчанию hello, который используется, если не указан фильтр при создании новой подписки.</span><span class="sxs-lookup"><span data-stu-id="5a305-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="5a305-139">Здравствуйте, когда **MatchAll** используется фильтр, раздел опубликованного toohello все сообщения помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="5a305-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="5a305-140">Hello следующем примере создается подписка с именем «AllMessages» и использует hello по умолчанию **MatchAll** фильтра.</span><span class="sxs-lookup"><span data-stu-id="5a305-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="5a305-141">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="5a305-141">Create subscriptions with filters</span></span>
<span data-ttu-id="5a305-142">Также можно создать фильтры, позволяющие tooscope сообщений отправила разделе tooa должно отображаться в рамках подписки определенный раздел.</span><span class="sxs-lookup"><span data-stu-id="5a305-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="5a305-143">Hello самый гибкий тип фильтра, поддерживаемых подписок — [SqlFilter][SqlFilter], который реализует подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="5a305-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="5a305-144">Фильтры SQL работают с свойств сообщений hello, раздел опубликованного toohello hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="5a305-145">Дополнительные сведения о выражениях hello, которые могут использоваться с фильтром SQL просмотрите hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="5a305-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="5a305-146">Hello следующий пример создает подписку с именем `HighMessages` с [SqlFilter] [ SqlFilter] объект, который выбирает только сообщения, которые содержат пользовательского **MessageNumber** свойство больше 3:</span><span class="sxs-lookup"><span data-stu-id="5a305-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="5a305-147">Аналогичным образом hello следующий пример создает подписку с именем `LowMessages` с [SqlFilter] [ SqlFilter] объект, который выбирает только сообщения, которые содержат **MessageNumber** Свойство меньше или равно too3:</span><span class="sxs-lookup"><span data-stu-id="5a305-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="5a305-148">Когда теперь отправляется сообщение слишком`TestTopic`, его будет всегда доставляться toohello tooreceivers подписка `AllMessages` подписки и выборочно доставленный tooreceivers подписка toohello `HighMessages` и `LowMessages` (подписки зависимости содержимое сообщения).</span><span class="sxs-lookup"><span data-stu-id="5a305-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="5a305-149">Отправить tooa темы о сообщениях</span><span class="sxs-lookup"><span data-stu-id="5a305-149">Send messages tooa topic</span></span>
<span data-ttu-id="5a305-150">приложение получает toosend раздела Service Bus сообщение tooa **ServiceBusContract** объекта.</span><span class="sxs-lookup"><span data-stu-id="5a305-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a305-151">Hello следующий код демонстрирует, как toosend сообщение hello `TestTopic` раздел создан ранее в рамках hello `HowToSample` пространство имен:</span><span class="sxs-lookup"><span data-stu-id="5a305-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="5a305-152">Сообщения, отправляемые разделы шины tooService, экземпляры [BrokeredMessage] [ BrokeredMessage] класса.</span><span class="sxs-lookup"><span data-stu-id="5a305-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5a305-153">[BrokeredMessage][BrokeredMessage]* объекты имеют ряд стандартных методов (например, **setLabel** и **TimeToLive**), словари, используемые toohold пользовательские Свойства приложения и текст из произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="5a305-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="5a305-154">Приложение может установить hello текст сообщения, передав в конструктор hello любой сериализуемый объект [BrokeredMessage][BrokeredMessage]и соответствующие hello **DataContractSerializer**  затем будет использоваться tooserialize hello объекта.</span><span class="sxs-lookup"><span data-stu-id="5a305-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="5a305-155">Кроме того, может быть предоставлен объект **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="5a305-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="5a305-156">Hello следующий пример демонстрирует способ тестирования toosend пяти сообщений toothe `TestTopic` **MessageSender** были получены в приведенном выше фрагменте кода hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="5a305-157">Обратите внимание, каким образом hello **MessageNumber** зависит от значения свойства каждого сообщения hello итерацию цикла hello (Это определяет, какие подписки получают его):</span><span class="sxs-lookup"><span data-stu-id="5a305-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="5a305-158">Темы Service Bus поддерживает максимальный размер сообщения 256 КБ в hello [стандартного уровня](service-bus-premium-messaging.md) и 1 МБ в hello [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5a305-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5a305-159">Hello заголовок, который включает hello standard и свойства пользовательского приложения, может иметь максимальный размер 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="5a305-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5a305-160">Нет ограничений на hello количество сообщений, которые содержатся в разделе, но имеется ограничение на общий размер сообщений hello, удерживаемые раздела hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="5a305-161">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="5a305-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="5a305-162">Способ tooreceive сообщений из подписки</span><span class="sxs-lookup"><span data-stu-id="5a305-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="5a305-163">tooreceive сообщения из подписки, используют **ServiceBusContract** объекта.</span><span class="sxs-lookup"><span data-stu-id="5a305-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a305-164">Полученные сообщения могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="5a305-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="5a305-165">При использовании hello **ReceiveAndDelete** режиме получение является единовременной операцией - то есть, Service Bus, получив запрос чтения для сообщения, он помечает приветственное сообщение как полученное и возвращает его toothe приложения.</span><span class="sxs-lookup"><span data-stu-id="5a305-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="5a305-166">**ReceiveAndDelete** режим — самая простая модель hello и лучше всего подходит для сценариев, в которых приложение может не обрабатывать сообщение hello в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="5a305-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5a305-167">toounderstand это, рассмотрим сценарий, в какие неполадки потребителя hello hello получают запрос и затем ломается до его обработки.</span><span class="sxs-lookup"><span data-stu-id="5a305-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5a305-168">Так как сообщение как полученное, затем при hello запустится и начинает получать сообщения снова будет помеченных Service Bus, оно пропустит сообщение hello, потребляет предыдущих toohello аварийного завершения.</span><span class="sxs-lookup"><span data-stu-id="5a305-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5a305-169">В **PeekLock** режиме получать становится операции два этапа, что делает его возможных toosupport приложений, которые не удается обработать отсутствующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a305-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5a305-170">Service Bus, получив запрос, он находит Далее toobe сообщение hello потребляет блокирует ее с tooprevent получения его другими получателями и возвращает его toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="5a305-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5a305-171">После того, как приложение hello завершает обработку сообщения hello (или хранит его для будущей обработки), его выполнить hello второго этапа hello процесс получения путем вызова **удалить** на полученных приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="5a305-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="5a305-172">Когда Service Bus обнаруживает hello **удалить** вызов, он пометить приветственное сообщение как полученное и удалите его из раздела hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="5a305-173">Hello приведенном ниже примере показано, как можно получать сообщения и обработанные с помощью **PeekLock** режиме (не hello по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="5a305-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="5a305-174">Hello пример выполняет цикл и обрабатывает сообщения в подписки «HighMessages» hello и затем завершается, если больше нет сообщений (Кроме того, могут быть заданы toowait для новых сообщений).</span><span class="sxs-lookup"><span data-stu-id="5a305-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5a305-175">Как происходит сбой toohandle приложения и может быть прочитан сообщений</span><span class="sxs-lookup"><span data-stu-id="5a305-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="5a305-176">Шина обслуживания предоставляет toohelp функциональные возможности, которые корректного восстановления после ошибок в приложении или затруднений при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="5a305-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5a305-177">Если приложение получатель не может tooprocess сообщение hello для какой-либо причине, то он может вызвать hello **unlockMessage** метод для получения приветственное сообщение (вместо hello **deleteMessage** метода).</span><span class="sxs-lookup"><span data-stu-id="5a305-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="5a305-178">Это сообщение hello toounlock Service Bus в пределах раздела hello и сделать ее доступной toobe получили еще раз, либо путем hello же потреблять приложение или другое приложение потребителя.</span><span class="sxs-lookup"><span data-stu-id="5a305-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5a305-179">Кроме того, есть таймаут, связанный с сообщения, заблокированного раздела и при сбое приложения hello tooprocess приветственное сообщение, прежде чем срок блокировки (например, если приложение hello терпит сбой), то служебной шины будет автоматическую разблокировку сообщения hello и сделать ее доступной toobe получили еще раз.</span><span class="sxs-lookup"><span data-stu-id="5a305-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5a305-180">В hello событие, которое hello приложение аварийно завершает работу после обработки сообщения hello, но перед hello **deleteMessage** выдается запрос, то при перезапуске приветственное сообщение будет повторно доставлены toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="5a305-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5a305-181">Это часто называется **по крайней мере после обработки**, то есть каждое сообщение обрабатывается хотя бы один раз, но в некоторых ситуациях hello же сообщение может доставляться.</span><span class="sxs-lookup"><span data-stu-id="5a305-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5a305-182">Если сценарий hello не допускает обработку дубликатов, разработчикам приложений следует добавить дополнительную логику tootheir приложения toohandle повторной доставке сообщений.</span><span class="sxs-lookup"><span data-stu-id="5a305-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="5a305-183">Это можно сделать с помощью hello **getMessageId** метод сообщения hello, который остается постоянным протяжении всех попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="5a305-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="5a305-184">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="5a305-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="5a305-185">Здравствуйте основной способ toodelete разделы и подписки — toouse **ServiceBusContract** объекта.</span><span class="sxs-lookup"><span data-stu-id="5a305-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a305-186">Удаление раздела приведет к удалению всех подписок, зарегистрированных в разделе hello.</span><span class="sxs-lookup"><span data-stu-id="5a305-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="5a305-187">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="5a305-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="5a305-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a305-188">Next Steps</span></span>
<span data-ttu-id="5a305-189">Теперь, когда вы узнали основы hello очереди шины обслуживания, в разделе [очереди Service Bus, разделы и подписки] [ Service Bus queues, topics, and subscriptions] для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="5a305-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
