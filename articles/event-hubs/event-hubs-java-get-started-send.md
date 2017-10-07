---
title: "tooAzure aaaSend событий концентраторов событий с помощью Java | Документы Microsoft"
description: "Начать отправку tooEvent концентраторы, с помощью Java"
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
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="bad46-103">Отправлять события tooAzure концентраторов событий, с помощью Java</span><span class="sxs-lookup"><span data-stu-id="bad46-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="bad46-104">Введение</span><span class="sxs-lookup"><span data-stu-id="bad46-104">Introduction</span></span>
<span data-ttu-id="bad46-105">Концентраторы событий — это система высокой степенью масштабирования приема, можно принять миллионов событий в секунду, включение tooprocess приложения и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="bad46-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="bad46-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="bad46-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="bad46-107">Дополнительные сведения см. в разделе hello [Обзор концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="bad46-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="bad46-108">В этом учебнике показано как концентратора событий tooan toosend событий с помощью консольного приложения на языке Java.</span><span class="sxs-lookup"><span data-stu-id="bad46-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="bad46-109">tooreceive события с помощью библиотеки hello узел обработчика событий Java, см. [в этой статье](event-hubs-java-get-started-receive-eph.md), или выберите соответствующий язык принимающей hello в левой таблице hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="bad46-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="bad46-110">В порядке toocomplete этого учебника требуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="bad46-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="bad46-111">Среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="bad46-111">A Java development environment.</span></span> <span data-ttu-id="bad46-112">Для этого руководства предполагается использование среды [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="bad46-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="bad46-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="bad46-113">An active Azure account.</span></span> <br/><span data-ttu-id="bad46-114">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="bad46-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="bad46-115">Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="bad46-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="bad46-116">Отправка сообщений tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="bad46-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="bad46-117">Hello клиентской библиотеки Java для концентраторов событий доступна для использования в проектах Maven из hello [Maven центральный репозиторий](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="bad46-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="bad46-118">Вы можете обратиться к этой библиотеке, с помощью объявления зависимостей в файле проекта Maven hello.</span><span class="sxs-lookup"><span data-stu-id="bad46-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="bad46-119">Для различных типов среды сборки c, можно явно загрузить файлы JAR hello последнего выпуска из hello [Maven центральный репозиторий](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="bad46-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="bad46-120">Для простых событий издателя импортировать hello *com.microsoft.azure.eventhubs* пакет для клиентских классов hello концентраторов событий и hello *com.microsoft.azure.servicebus* пакета программа классов, например как общие исключения, которые являются общими с клиентом обмена сообщениями Azure Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="bad46-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="bad46-121">Для следующих образец hello сначала необходимо создайте новый проект Maven для приложений консоли или оболочки в избранные среда разработки Java.</span><span class="sxs-lookup"><span data-stu-id="bad46-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="bad46-122">Имя класса hello `Send`.</span><span class="sxs-lookup"><span data-stu-id="bad46-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="bad46-123">Замените имена hub hello пространства имен и событие hello значения, используемые при создании концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="bad46-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="bad46-124">Затем создайте одиночное событие, преобразовав строку в байтовую кодировку UTF-8.</span><span class="sxs-lookup"><span data-stu-id="bad46-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="bad46-125">Затем создайте новый экземпляр клиента концентраторов событий из строки подключения hello и отправить сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="bad46-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="bad46-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bad46-126">Next steps</span></span>
<span data-ttu-id="bad46-127">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="bad46-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="bad46-128">Получение событий с помощью hello EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="bad46-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="bad46-129">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="bad46-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="bad46-130">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="bad46-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="bad46-131">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="bad46-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md