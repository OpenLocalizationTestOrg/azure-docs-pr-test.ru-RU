---
title: "Отправка событий в концентраторы событий Azure с помощью Java | Документация Майкрософт"
description: "Начало работы с отправкой в концентраторы событий с помощью Java."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="05a48-103">Отправка событий в концентраторы событий Azure с помощью Java</span><span class="sxs-lookup"><span data-stu-id="05a48-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="05a48-104">Введение</span><span class="sxs-lookup"><span data-stu-id="05a48-104">Introduction</span></span>
<span data-ttu-id="05a48-105">Концентраторы событий — это высокомасштабируемая система, способная принимать миллионы событий в секунду, благодаря которой приложения могут обрабатывать и анализировать большие объемы данных от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="05a48-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="05a48-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="05a48-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="05a48-107">Дополнительные сведения см. в [обзоре концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="05a48-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="05a48-108">В этом руководстве показано, как отправлять события в концентратор событий с помощью консольного приложения на языке Java.</span><span class="sxs-lookup"><span data-stu-id="05a48-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="05a48-109">Дополнительные сведения о получении событий с помощью библиотеки узла обработчика событий для Java см. в [этой статье](event-hubs-java-get-started-receive-eph.md), или выберите соответствующий язык в оглавлении статьи слева.</span><span class="sxs-lookup"><span data-stu-id="05a48-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="05a48-110">Чтобы выполнить задания из этого учебника, вам нужно следующее:</span><span class="sxs-lookup"><span data-stu-id="05a48-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="05a48-111">Среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="05a48-111">A Java development environment.</span></span> <span data-ttu-id="05a48-112">Для этого руководства предполагается использование среды [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="05a48-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="05a48-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="05a48-113">An active Azure account.</span></span> <br/><span data-ttu-id="05a48-114">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="05a48-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="05a48-115">Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="05a48-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="05a48-116">Отправка сообщений в центры событий</span><span class="sxs-lookup"><span data-stu-id="05a48-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="05a48-117">Клиентскую библиотеку Java для концентраторов событий можно использовать в проектах Maven из [центрального репозитория Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="05a48-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="05a48-118">Чтобы сослаться на эту библиотеку, используйте следующее объявление зависимостей в файле проекта Maven:</span><span class="sxs-lookup"><span data-stu-id="05a48-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="05a48-119">Для различных типов сред сборки можно явно получить последние выпущенные JAR-файлы из [центрального репозитория Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="05a48-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="05a48-120">Если используется простой издатель событий, импортируйте пакет *com.microsoft.azure.eventhubs* для клиентских классов концентраторов событий и пакет *com.microsoft.azure.servicebus* для служебных классов, таких как общие исключения, которые используются совместно с клиентом обмена сообщениями служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="05a48-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="05a48-121">Следующий пример сначала создает новый проект Maven для приложения консоли или оболочки в избранной среде разработки Java.</span><span class="sxs-lookup"><span data-stu-id="05a48-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="05a48-122">Назовите класс `Send`.</span><span class="sxs-lookup"><span data-stu-id="05a48-122">Name the class `Send`.</span></span>     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="05a48-123">Замените имя пространства имен и концентратора событий значениями, использованными при создании концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="05a48-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="05a48-124">Затем создайте одиночное событие, преобразовав строку в байтовую кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="05a48-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="05a48-125">Затем создайте новый экземпляр клиента концентраторов событий из строки подключения и отправьте сообщение.</span><span class="sxs-lookup"><span data-stu-id="05a48-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="05a48-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05a48-126">Next steps</span></span>
<span data-ttu-id="05a48-127">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="05a48-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="05a48-128">[Receive events using the EventProcessorHost](event-hubs-java-get-started-receive-eph.md) (Получение событий с помощью EventProcessorHost)</span><span class="sxs-lookup"><span data-stu-id="05a48-128">[Receive events using the EventProcessorHost](event-hubs-java-get-started-receive-eph.md)</span></span>
* <span data-ttu-id="05a48-129">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="05a48-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="05a48-130">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="05a48-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="05a48-131">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="05a48-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md