---
title: "Как использовать разделы служебной шины Azure с помощью Java | Документация Майкрософт"
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
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="e1448-103">Как использовать разделы и подписки служебной шины с Java</span><span class="sxs-lookup"><span data-stu-id="e1448-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="e1448-104">В этом руководстве описывается использование разделов и подписок служебной шины.</span><span class="sxs-lookup"><span data-stu-id="e1448-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="e1448-105">Примеры написаны на Java и используют [пакет Azure SDK для Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="e1448-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="e1448-106">В этой статье описаны такие сценарии, как **создание разделов и подписок**, **создание фильтров подписок**, **отправка сообщений в раздел**, **получение сообщений из подписки** и **удаление разделов и подписок**.</span><span class="sxs-lookup"><span data-stu-id="e1448-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="e1448-107">Что такое разделы и подписки служебной шины?</span><span class="sxs-lookup"><span data-stu-id="e1448-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="e1448-108">Разделы и подписки служебной шины поддерживают модель обмена сообщениями " *публикация и подписка* ".</span><span class="sxs-lookup"><span data-stu-id="e1448-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="e1448-109">При использовании разделов и подписок компоненты распределенного приложения не взаимодействуют между собой напрямую, а обмениваются сообщениями через раздел, который выступает в качестве посредника.</span><span class="sxs-lookup"><span data-stu-id="e1448-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="e1448-111">В отличие от очередей служебной шины, где каждое сообщение обрабатывается одним потребителем, разделы и подписки предоставляют вид связи одного со многими с помощью шаблона публикации/подписки.</span><span class="sxs-lookup"><span data-stu-id="e1448-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="e1448-112">Можно зарегистрировать несколько подписок на раздел.</span><span class="sxs-lookup"><span data-stu-id="e1448-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="e1448-113">Когда сообщение отправляется в раздел, оно затем может обрабатываться независимо каждой подпиской.</span><span class="sxs-lookup"><span data-stu-id="e1448-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="e1448-114">Раздел подписки напоминает виртуальную очередь, которая получает копии сообщений, отправленных в раздел.</span><span class="sxs-lookup"><span data-stu-id="e1448-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="e1448-115">Вы можете зарегистрировать правила фильтрации для раздела на основе подписки, которые позволят указать, какие сообщения и от каких подписок могут быть получены разделом.</span><span class="sxs-lookup"><span data-stu-id="e1448-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="e1448-116">Разделы и подписки Service Bus обеспечивают возможность масштабирования для обработки очень большого количества сообщений для очень большого количества пользователей и приложений.</span><span class="sxs-lookup"><span data-stu-id="e1448-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="e1448-117">Создание пространства имен службы</span><span class="sxs-lookup"><span data-stu-id="e1448-117">Create a service namespace</span></span>
<span data-ttu-id="e1448-118">Чтобы начать использование разделов и подписок служебной шины в Azure, необходимо сначала создать пространство имен, которое предоставляет контейнер, предназначенный для ресурсов служебной шины в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="e1448-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="e1448-119">Создание пространства имен службы:</span><span class="sxs-lookup"><span data-stu-id="e1448-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="e1448-120">Настройка приложения для использования служебной шины</span><span class="sxs-lookup"><span data-stu-id="e1448-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="e1448-121">Перед созданием этого образца убедитесь, что вы установили [пакет Azure SDK для Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="e1448-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="e1448-122">При использовании Eclipse можно установить [набор средств Azure для Eclipse][Azure Toolkit for Eclipse], включающий в себя пакет Azure SDK для Java.</span><span class="sxs-lookup"><span data-stu-id="e1448-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="e1448-123">Затем можно добавить **библиотеки Microsoft Azure для Java** в проект.</span><span class="sxs-lookup"><span data-stu-id="e1448-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="e1448-124">Добавьте в начало Java-файла следующие инструкции `import`:</span><span class="sxs-lookup"><span data-stu-id="e1448-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="e1448-125">Добавьте библиотеки Azure для Java в путь построения и включите его в сборку развертывания проекта.</span><span class="sxs-lookup"><span data-stu-id="e1448-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="e1448-126">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="e1448-126">Create a topic</span></span>
<span data-ttu-id="e1448-127">Операции управления для разделов служебной шины можно выполнять с помощью класса **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="e1448-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="e1448-128">Объект **ServiceBusContract** создается с соответствующей конфигурацией, которая инкапсулирует маркер SAS с разрешениями на управление им, а класс **ServiceBusContract** является единственной точкой связи с Azure.</span><span class="sxs-lookup"><span data-stu-id="e1448-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="e1448-129">Класс **ServiceBusService** предоставляет методы для создания, перечисления и удаления разделов.</span><span class="sxs-lookup"><span data-stu-id="e1448-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="e1448-130">В следующем примере показано, как можно использовать объект **ServiceBusService** для создания раздела с именем `TestTopic` и пространством имен `HowToSample`.</span><span class="sxs-lookup"><span data-stu-id="e1448-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="e1448-131">Методы **TopicInfo** позволяют настроить свойства раздела (например, задавать значение срока жизни (TTL) по умолчанию, применяемое к сообщениям, отправленным в раздел).</span><span class="sxs-lookup"><span data-stu-id="e1448-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="e1448-132">Следующий пример показывает, как создать раздел с именем `TestTopic` и размером не более 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e1448-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="e1448-133">Обратите внимание, что метод **listTopics** можно использовать для объектов **ServiceBusContract**, чтобы проверить, существует ли уже раздел с указанным именем в пространстве имен службы.</span><span class="sxs-lookup"><span data-stu-id="e1448-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="e1448-134">Создание подписок</span><span class="sxs-lookup"><span data-stu-id="e1448-134">Create subscriptions</span></span>
<span data-ttu-id="e1448-135">Подписки на разделы также создаются с помощью класса **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="e1448-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="e1448-136">Подписки имеют имена и могут использовать дополнительный фильтр, ограничивающий набор сообщений, доставляемых в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="e1448-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="e1448-137">Создание подписки с фильтром по умолчанию (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="e1448-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="e1448-138">Фильтр **MatchAll** является фильтром по умолчанию, используемым, если при создании новой подписки не указан фильтр.</span><span class="sxs-lookup"><span data-stu-id="e1448-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="e1448-139">Если используется фильтр **MatchAll**, то все сообщения, опубликованные в разделе, помещаются в виртуальную очередь подписки.</span><span class="sxs-lookup"><span data-stu-id="e1448-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="e1448-140">В следующем примере создается подписка AllMessages и используется фильтр по умолчанию **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="e1448-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="e1448-141">Создание подписок с фильтрами</span><span class="sxs-lookup"><span data-stu-id="e1448-141">Create subscriptions with filters</span></span>
<span data-ttu-id="e1448-142">Вы также можете создать фильтры, позволяющие определять, какие сообщения, отправленные в раздел, будут отображаться в определенной подписке раздела.</span><span class="sxs-lookup"><span data-stu-id="e1448-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="e1448-143">Самый гибкий тип фильтра, который поддерживается подписками, — это [SqlFilter][SqlFilter], реализующий подмножество SQL92.</span><span class="sxs-lookup"><span data-stu-id="e1448-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="e1448-144">Фильтры SQL работают со свойствами сообщений, которые опубликованы в разделе.</span><span class="sxs-lookup"><span data-stu-id="e1448-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="e1448-145">Дополнительные сведения о выражениях, которые можно использовать с фильтром SQL, см. в описании синтаксиса [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="e1448-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="e1448-146">В следующем примере создается подписка `HighMessages`, содержащая объект [SqlFilter][SqlFilter], который выбирает только сообщения, значение настраиваемого свойства **MessageNumber** которых превышает 3.</span><span class="sxs-lookup"><span data-stu-id="e1448-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="e1448-147">Аналогично в следующем примере создается подписка `LowMessages` с фильтром [SqlFilter][SqlFilter], который выбирает только те сообщения, у которых значение свойства **MessageNumber** меньше или равно 3.</span><span class="sxs-lookup"><span data-stu-id="e1448-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="e1448-148">Если сообщение отправляется в раздел `TestTopic`, то оно всегда будет доставляться в приемники, подписанные на `AllMessages`, и в отдельные приемники, подписанные на `HighMessages` и `LowMessages` (в зависимости от содержимого сообщений).</span><span class="sxs-lookup"><span data-stu-id="e1448-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="e1448-149">Отправка сообщений в раздел</span><span class="sxs-lookup"><span data-stu-id="e1448-149">Send messages to a topic</span></span>
<span data-ttu-id="e1448-150">Чтобы отправить сообщение в раздел служебной шины, приложение получает объект **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="e1448-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="e1448-151">В следующем примере кода показано, как отправить сообщение в раздел `TestTopic`, созданный ранее в пространстве имен `HowToSample`.</span><span class="sxs-lookup"><span data-stu-id="e1448-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="e1448-152">Сообщения, отправляемые в разделы служебной шины, — это экземпляры класса [BrokeredMessage][BrokeredMessage].</span><span class="sxs-lookup"><span data-stu-id="e1448-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="e1448-153">Объекты [BrokeredMessage][BrokeredMessage]* имеют набор стандартных методов (например, **setLabel** и **TimeToLive**), словарь, используемый для хранения настраиваемых свойств приложения, и текст из произвольных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="e1448-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="e1448-154">Приложение может задать текст сообщения, передав конструктору [BrokeredMessage][BrokeredMessage] любой сериализуемый объект, после чего для сериализации объекта будет использоваться соответствующий **DataContractSerializer**.</span><span class="sxs-lookup"><span data-stu-id="e1448-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="e1448-155">Кроме того, может быть предоставлен объект **java.io.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="e1448-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="e1448-156">В следующем примере показано, как отправить пять тестовых сообщений в очередь `TestTopic` объекта **MessageSender**, полученного в предыдущем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="e1448-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="e1448-157">Обратите внимание, что значение свойства **MessageNumber** всех сообщений зависит от итерации цикла (определяет, какие подписки получают их).</span><span class="sxs-lookup"><span data-stu-id="e1448-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="e1448-158">Разделы служебной шины поддерживают максимальный размер сообщения 256 КБ для [уровня "Стандартный"](service-bus-premium-messaging.md) и 1 МБ для [уровня Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="e1448-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="e1448-159">Максимальный размер заголовка, который содержит стандартные и настраиваемые свойства приложения, — 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="e1448-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="e1448-160">Ограничения количества сообщений в разделе нет, но есть максимальный общий размер сообщений, содержащихся в разделе.</span><span class="sxs-lookup"><span data-stu-id="e1448-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="e1448-161">Этот размер раздела определяется при создании с верхним пределом 5 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e1448-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="e1448-162">Как получать сообщения из подписки</span><span class="sxs-lookup"><span data-stu-id="e1448-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="e1448-163">Чтобы получить сообщения из подписки, используйте объект **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="e1448-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="e1448-164">Полученные сообщения могут работать в двух различных режимах: **ReceiveAndDelete** и **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="e1448-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="e1448-165">При использовании режима **ReceiveAndDelete** получение является одиночной операцией, т. е. когда служебная шина получает запрос на чтение для сообщения в подписке, сообщение помечается как использованное и возвращается в приложение.</span><span class="sxs-lookup"><span data-stu-id="e1448-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="e1448-166">Режим **ReceiveAndDelete** представляет собой самую простую модель, которая лучше всего работает в ситуациях, когда приложение может не обрабатывать сообщение при сбое.</span><span class="sxs-lookup"><span data-stu-id="e1448-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="e1448-167">Чтобы это понять, рассмотрим сценарий, в котором объект-получатель выдает запрос на получение и выходит из строя до его обработки.</span><span class="sxs-lookup"><span data-stu-id="e1448-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="e1448-168">Поскольку служебная шина помечает сообщение как использованное, то когда после своего перезапуска приложение снова начнет обрабатывать сообщения, оно пропустит сообщение, использованное до сбоя.</span><span class="sxs-lookup"><span data-stu-id="e1448-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="e1448-169">В режиме **PeekLock** процесс получения становится двухэтапной операцией, что позволяет поддерживать приложения, неустойчивые к пропуску сообщений.</span><span class="sxs-lookup"><span data-stu-id="e1448-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="e1448-170">Получив запрос, служебная шина находит следующее сообщение, блокирует его, чтобы предотвратить его получение другими получателями, и возвращает его приложению.</span><span class="sxs-lookup"><span data-stu-id="e1448-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="e1448-171">Когда приложение завершает обработку сообщения (или сохраняет его для будущей обработки), оно завершает второй этап процесса получения, вызывая метод **Delete** для полученного сообщения.</span><span class="sxs-lookup"><span data-stu-id="e1448-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="e1448-172">Когда служебная шина обнаруживает вызов **Delete**, она помечает сообщение как использованное и удаляет его из раздела.</span><span class="sxs-lookup"><span data-stu-id="e1448-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="e1448-173">В примере ниже показано, как получать и обрабатывать сообщения с помощью режима **PeekLock** (не используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="e1448-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="e1448-174">В следующем примере выполняется цикл и обрабатывает сообщения в подписке «HighMessages», а затем завершает работу, когда больше нет сообщений (Кроме того, можно настроить ожидание новых сообщений).</span><span class="sxs-lookup"><span data-stu-id="e1448-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

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
            // Display the topic message.
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
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="e1448-175">Как обрабатывать сбои приложения и нечитаемые сообщения</span><span class="sxs-lookup"><span data-stu-id="e1448-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="e1448-176">служебная шина предоставляет функции, помогающие корректно выполнить восстановление после ошибок в приложении или трудностей, возникших при обработке сообщения.</span><span class="sxs-lookup"><span data-stu-id="e1448-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="e1448-177">Если приложение-получатель по каким-либо причинам не может обработать сообщение, то оно может вызвать для полученного сообщения метод **unlockMessage** (вместо метода **deleteMessage**).</span><span class="sxs-lookup"><span data-stu-id="e1448-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="e1448-178">После этого служебная шина разблокирует сообщение в разделе и сделает его доступным для приема тем же или другим приложением-пользователем.</span><span class="sxs-lookup"><span data-stu-id="e1448-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="e1448-179">Кроме того, с сообщением, заблокированным в разделе, связано время ожидания. Если приложение не сможет обработать сообщение в течение времени ожидания (например, при сбое приложения), то служебная шина разблокирует сообщение автоматически и сделает его доступным для приема.</span><span class="sxs-lookup"><span data-stu-id="e1448-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="e1448-180">Если сбой приложения происходит после обработки сообщения, но перед отправкой запроса **deleteMessage** это сообщение будет повторно доставлено в приложение после его перезапуска.</span><span class="sxs-lookup"><span data-stu-id="e1448-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="e1448-181">Часто этот подход называют **обработать хотя бы один раз**, т. е. каждое сообщение будет обрабатываться по крайней мере один раз, но в некоторых случаях это же сообщение может быть доставлено повторно.</span><span class="sxs-lookup"><span data-stu-id="e1448-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="e1448-182">Если повторная обработка недопустима, разработчики приложения должны добавить дополнительную логику для обработки повторной доставки сообщений.</span><span class="sxs-lookup"><span data-stu-id="e1448-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="e1448-183">Часто это достигается с помощью метода **getMessageId** сообщения, которое остается постоянным для различных попыток доставки.</span><span class="sxs-lookup"><span data-stu-id="e1448-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="e1448-184">Удаление разделов и подписок</span><span class="sxs-lookup"><span data-stu-id="e1448-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="e1448-185">Основным способом удаления разделов и подписок является использование объекта **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="e1448-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="e1448-186">При удалении раздела также удаляются все подписки, зарегистрированные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e1448-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="e1448-187">Подписки также можно удалять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="e1448-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="e1448-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1448-188">Next Steps</span></span>
<span data-ttu-id="e1448-189">Вы познакомились с основами использования очередей служебной шины. Дополнительные сведения см. в статье [Очереди, разделы и подписки служебной шины][Service Bus queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="e1448-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
