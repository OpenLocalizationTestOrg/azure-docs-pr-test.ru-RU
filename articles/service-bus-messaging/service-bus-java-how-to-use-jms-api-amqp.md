---
title: "toouse aaaHow AMQP 1.0 с помощью API служебной шины Java hello | Документы Microsoft"
description: "Как toouse hello службу сообщений Java (JMS) с Azure Service Bus и Advanced Message Queuing Protodol (AMQP) 1.0."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="cf0ac-103">Как toouse hello службу сообщений Java (JMS) API с Service Bus и AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="cf0ac-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="cf0ac-104">Hello Advanced Message Queuing Protocol (AMQP) 1.0 — это эффективный, надежный, транспортного уровня протокол, которые можно использовать toobuild надежных кроссплатформенных приложений обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="cf0ac-105">Поддержка AMQP 1.0 в шине обслуживания означает, что можно использовать hello очереди и публикации или подписки через посредника функций обмена сообщениями из диапазона различных платформ, используя эффективный двоичный протокол.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="cf0ac-106">Кроме того, можно создавать приложения, содержащие компоненты, созданные с использованием разнообразных языков, платформ и операционных систем.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="cf0ac-107">В этой статье объясняется, как toouse Service Bus функций обмена сообщениями (очередей и публикации или подписки разделов) из приложений Java с помощью hello популярных службу сообщений Java (JMS) стандартный API.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="cf0ac-108">Отсутствует [сопутствующая статья](service-bus-amqp-dotnet.md) , объясняется, как toodo hello же с помощью hello API .NET служебной шины.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="cf0ac-109">Можно использовать эти два руководства по вместе toolearn, об обмене сообщениями между различными платформами, с помощью AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="cf0ac-110">Приступая к работе со служебной шиной</span><span class="sxs-lookup"><span data-stu-id="cf0ac-110">Get started with Service Bus</span></span>
<span data-ttu-id="cf0ac-111">В этом руководстве предполагается, что вы уже создали пространство имен служебной шины, содержащее очередь с именем **queue1**.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="cf0ac-112">Если этого не сделать, то вы можете [создать пространство имен hello и очереди](service-bus-create-namespace-portal.md) с помощью hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cf0ac-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cf0ac-113">Дополнительные сведения о том, как отображается toocreate пространства имен служебной шины и очереди, [приступить к работе с очередями Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="cf0ac-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cf0ac-114">Секционированные очереди и разделы также поддерживают AMQP.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="cf0ac-115">Дополнительные сведения см. в статьях [Секционированные сущности обмена сообщениями](service-bus-partitioning.md) и [Поддержка AMQP 1.0 для секционированных очередей и разделов служебной шины](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf0ac-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="cf0ac-116">Загрузка клиентской библиотеки AMQP 1.0 JMS hello</span><span class="sxs-lookup"><span data-stu-id="cf0ac-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="cf0ac-117">Сведения о котором toodownload hello последнюю версию клиентской библиотеки Apache Qpid JMS AMQP 1.0 hello [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="cf0ac-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="cf0ac-118">Необходимо добавить следующие четыре JAR-файла из toohello архива распространения Apache Qpid JMS AMQP 1.0 hello Java CLASSPATH при построении и запуске приложений JMS с Service Bus hello:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="cf0ac-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="cf0ac-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="cf0ac-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="cf0ac-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="cf0ac-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="cf0ac-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="cf0ac-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="cf0ac-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="cf0ac-123">Создание приложений Java</span><span class="sxs-lookup"><span data-stu-id="cf0ac-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="cf0ac-124">Интерфейс JNDI</span><span class="sxs-lookup"><span data-stu-id="cf0ac-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="cf0ac-125">JMS использует hello именования Java и каталог интерфейс JNDI toocreate разделение логических и физических имен.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="cf0ac-126">С помощью JNDI разрешаются два типа объектов JMS: ConnectionFactory и Destination.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="cf0ac-127">JNDI использует модель поставщика, в которую можно подключить разрешения имен установки toohandle служб другой каталог.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="cf0ac-128">Hello Apache Qpid JMS AMQP 1.0 библиотеки поставляется с простых свойств файловых JNDI поставщика, который настраивается с помощью файла свойств hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="cf0ac-129">Настройка hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="cf0ac-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="cf0ac-130">Здравствуйте записи, используемой toodefine **ConnectionFactory** в hello Qpid JNDI поставщик свойств файла имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="cf0ac-131">Где **[jndi_name]** и **[ConnectionURL]** имеют hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="cf0ac-132">**[jndi_name]** : hello логическое имя hello ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="cf0ac-133">Это имя hello, который будет разрешен в hello приложения Java, с помощью метода JNDI IntialContext.lookup() hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="cf0ac-134">**[ConnectionURL]** : URL-адрес, предоставляющий библиотеке JMS hello сведениями hello необходимые toohello брокера AMQP.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="cf0ac-135">Формат Hello hello **ConnectionURL** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="cf0ac-136">Где **[пространство имен]**, **[SASPolicyName]** и **[SASPolicyKey]** имеют hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="cf0ac-137">**[пространство имен]** : hello пространства имен Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="cf0ac-138">**[SASPolicyName]** : hello имя политики очереди подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="cf0ac-139">**[SASPolicyKey]** : hello ключ политики очереди подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="cf0ac-140">URL-кодирование пароля hello необходимо вручную.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="cf0ac-141">Полезная служебная программа URL-кодирования доступна по адресу [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="cf0ac-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="cf0ac-142">Настройка назначений</span><span class="sxs-lookup"><span data-stu-id="cf0ac-142">Configure destinations</span></span>
<span data-ttu-id="cf0ac-143">Здравствуйте, toodefine запись, используемая для копирования в поставщик JNDI файла свойств Qpid hello данных является hello следующая формата:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="cf0ac-144">или</span><span class="sxs-lookup"><span data-stu-id="cf0ac-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="cf0ac-145">Где **[jndi\_имя]** и **[физического\_имя]** имеют hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="cf0ac-146">**[jndi_name]** : hello логическое имя назначения «hello».</span><span class="sxs-lookup"><span data-stu-id="cf0ac-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="cf0ac-147">Это имя hello, который будет разрешен в hello приложения Java, с помощью метода JNDI IntialContext.lookup() hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="cf0ac-148">**[physical_name]** : имя hello hello приложения hello toowhich сущности служебной шины отправлять или получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="cf0ac-149">При получении из подписки раздела Service Bus hello физическое имя, указанное в JNDI следует hello имя раздела hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="cf0ac-150">имя подписки Hello предоставляется при создании устойчивой подписки hello в коде приложения JMS hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="cf0ac-151">Hello [Service Bus AMQP 1.0 руководство разработчика](service-bus-amqp-dotnet.md) содержатся дополнительные сведения о работе с разделы служебной шины из JMS.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="cf0ac-152">Написать приложение hello JMS</span><span class="sxs-lookup"><span data-stu-id="cf0ac-152">Write hello JMS application</span></span>
<span data-ttu-id="cf0ac-153">Не существует специальных API-интерфейсов или параметров для использования JMS с Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="cf0ac-154">Однако существует несколько ограничений, которые будут рассмотрены ниже.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="cf0ac-155">Как и любого приложения JMS hello первое, что необходимые конфигурации среды JNDI hello, может tooresolve toobe **ConnectionFactory** и назначения.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="cf0ac-156">Настройка hello JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="cf0ac-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="cf0ac-157">Hello среды JNDI настраивается путем передачи хэш-таблицу сведений о конфигурации в конструктор hello класса javax.naming.InitialContext hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="cf0ac-158">Hello двумя обязательными элементами в хэш-таблице hello: имя класса hello hello начальной фабрики контекста и hello URL-адрес поставщика.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="cf0ac-159">Hello следующий код показывает, как tooconfigure hello JNDI toouse hello Qpid свойства файла среды на основе поставщика JNDI с свойства файл с именем **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="cf0ac-160">Простое приложение JMS, использующее очередь служебной шины</span><span class="sxs-lookup"><span data-stu-id="cf0ac-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="cf0ac-161">Hello следующий пример программы очереди Service Bus tooa JMS TextMessages с hello JNDI логическое имя очереди, отправляет и получает сообщения hello обратно.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a><span data-ttu-id="cf0ac-162">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="cf0ac-162">Run hello application</span></span>
<span data-ttu-id="cf0ac-163">Запуск приложения hello выводятся данные hello формы:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-163">Running hello application produces output of hello form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="cf0ac-164">Межплатформенный обмен сообщениями между JMS и .NET</span><span class="sxs-lookup"><span data-stu-id="cf0ac-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="cf0ac-165">В этом руководстве показано, как toosend и получать сообщения tooand с Service Bus с помощью JMS.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="cf0ac-166">Одним из ключевых преимуществ hello AMQP 1.0 то, что позволяет приложениям toobe, построенная для компонентов, написанных на разных языках с сообщения, которыми обмениваются надежно и с полной точностью.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="cf0ac-167">С помощью JMS hello демонстрационного приложения, описанного выше и аналогичные приложения .NET, взяты из сопутствующая статья [с использованием служебной шины из .NET с AMQP 1.0](service-bus-amqp-dotnet.md), обмен сообщениями между .NET и Java.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="cf0ac-168">Эта статья Дополнительные сведения о hello кросс платформенных обмена сообщениями с использованием Service Bus и AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="cf0ac-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="cf0ac-169">JMS too.NET</span></span>
<span data-ttu-id="cf0ac-170">toodemonstrate JMS too.NET обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="cf0ac-171">Запустите приложение образец hello .NET без аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="cf0ac-172">Запустите образец приложения Java hello с аргументом командной строки «sendonly» hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="cf0ac-173">В этом режиме hello приложения не будут получать сообщения из очереди hello, он будет отправлять.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="cf0ac-174">Нажмите клавишу **ввод** несколько раз в консоли приложения hello Java, которое может вызвать toobe сообщения отправляются.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="cf0ac-175">Эти сообщения принимаются hello приложения .NET.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="cf0ac-176">Вывод приложения JMS</span><span class="sxs-lookup"><span data-stu-id="cf0ac-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="cf0ac-177">Вывод приложения .NET</span><span class="sxs-lookup"><span data-stu-id="cf0ac-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="cf0ac-178">.NET tooJMS</span><span class="sxs-lookup"><span data-stu-id="cf0ac-178">.NET tooJMS</span></span>
<span data-ttu-id="cf0ac-179">tooJMS .NET toodemonstrate обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="cf0ac-180">Запустите пример приложения hello .NET с помощью аргумента командной строки «sendonly» hello.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="cf0ac-181">В этом режиме hello приложения не будут получать сообщения из очереди hello, он будет отправлять.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="cf0ac-182">Запустите приложение образец hello Java без аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="cf0ac-183">Нажмите клавишу **ввод** несколько раз в консоли приложения hello .NET, что приведет к toobe сообщения отправляются.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="cf0ac-184">Эти сообщения принимаются hello приложения Java.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="cf0ac-185">Вывод приложения .NET</span><span class="sxs-lookup"><span data-stu-id="cf0ac-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="cf0ac-186">Вывод приложения JMS</span><span class="sxs-lookup"><span data-stu-id="cf0ac-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="cf0ac-187">Неподдерживаемые возможности и ограничения</span><span class="sxs-lookup"><span data-stu-id="cf0ac-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="cf0ac-188">При использовании JMS через протокол AMQP 1.0 с Service Bus, а именно существуют Hello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="cf0ac-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="cf0ac-189">Для одного **сеанса** допускается только один **MessageProducer** или **MessageConsumer**.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="cf0ac-190">Если вам требуется toocreate несколько **MessageProducers** или **MessageConsumers** в приложении, создать выделенную **сеанса** для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="cf0ac-191">Временные подписки раздела в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="cf0ac-192">**MessageSelectors** сейчас не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="cf0ac-193">Временные назначения; например **TemporaryQueue**, **TemporaryTopic** не поддерживаются в настоящее время, а также hello **QueueRequestor** и **TopicRequestor**API, использовать их.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="cf0ac-194">Сеансы транзакций и распределенные транзакции не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="cf0ac-195">Сводка</span><span class="sxs-lookup"><span data-stu-id="cf0ac-195">Summary</span></span>
<span data-ttu-id="cf0ac-196">Это как tooguide было показано, как toouse через посредника Service Bus функций обмена сообщениями (очередей и публикации или подписки разделов) с помощью Java hello популярные API JMS и AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="cf0ac-197">Протокол AMQP 1.0 Service Bus можно также использовать из других языков, в числе которых .NET, C, Python и PHP.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="cf0ac-198">Компоненты, созданные с помощью этих разных языков могут обмениваться сообщениями надежно и с полной точностью, с помощью поддержки hello AMQP 1.0 в шине обслуживания.</span><span class="sxs-lookup"><span data-stu-id="cf0ac-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf0ac-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf0ac-199">Next steps</span></span>
* [<span data-ttu-id="cf0ac-200">Поддержка AMQP 1.0 в служебной шине</span><span class="sxs-lookup"><span data-stu-id="cf0ac-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="cf0ac-201">Как toouse AMQP 1.0 с hello API .NET служебной шины</span><span class="sxs-lookup"><span data-stu-id="cf0ac-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="cf0ac-202">Руководство разработчика AMQP 1.0 для служебной шины</span><span class="sxs-lookup"><span data-stu-id="cf0ac-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="cf0ac-203">Начало работы с очередями служебной шины</span><span class="sxs-lookup"><span data-stu-id="cf0ac-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="cf0ac-204">Центр разработчиков Java</span><span class="sxs-lookup"><span data-stu-id="cf0ac-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

