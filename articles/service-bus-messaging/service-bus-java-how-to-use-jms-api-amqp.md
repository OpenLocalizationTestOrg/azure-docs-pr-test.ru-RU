---
title: "Как использовать AMQP 1.0 с API служебной шины Java | Документация Майкрософт"
description: "Как использовать службу сообщений Java (JMS) со служебной шиной Azure и протоколом AMQP 1.0."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="19be0-103">Как использовать API службы сообщений Java (JMS) со служебной шиной и AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="19be0-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="19be0-104">AMQP 1.0 — это эффективный и надежный протокол обмена сообщениями на уровне соединения, который можно использовать для создания надежных кроссплатформенных приложений для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="19be0-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="19be0-105">Поддержка AMQP 1.0 в Service Bus означает, что с помощью эффективного двоичного протокола можно на различных платформах использовать возможности очередей и обмена сообщениями с публикацией/подпиской у брокера.</span><span class="sxs-lookup"><span data-stu-id="19be0-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="19be0-106">Кроме того, можно создавать приложения, содержащие компоненты, созданные с использованием разнообразных языков, платформ и операционных систем.</span><span class="sxs-lookup"><span data-stu-id="19be0-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="19be0-107">В этой статье описывается использование функций обмена сообщениями через служебную шину (очередей и публикации разделов или подписки на них) из приложений Java, использующих популярный стандарт API JMS.</span><span class="sxs-lookup"><span data-stu-id="19be0-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="19be0-108">В [связанной статье](service-bus-amqp-dotnet.md) объясняется, как выполнить те же действия, используя API .NET служебной шины.</span><span class="sxs-lookup"><span data-stu-id="19be0-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="19be0-109">Эти два руководства можно использовать совместно для изучения обмена сообщениями между различными платформами с помощью AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="19be0-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="19be0-110">Приступая к работе со служебной шиной</span><span class="sxs-lookup"><span data-stu-id="19be0-110">Get started with Service Bus</span></span>
<span data-ttu-id="19be0-111">В этом руководстве предполагается, что вы уже создали пространство имен служебной шины, содержащее очередь с именем **queue1**.</span><span class="sxs-lookup"><span data-stu-id="19be0-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="19be0-112">Если это не так, можно [создать пространство имен и очередь](service-bus-create-namespace-portal.md), используя [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19be0-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="19be0-113">Дополнительные сведения о создании пространства имен и очередей служебной шины см. в статье [Приступая к работе с очередями служебной шины](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="19be0-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="19be0-114">Секционированные очереди и разделы также поддерживают AMQP.</span><span class="sxs-lookup"><span data-stu-id="19be0-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="19be0-115">Дополнительные сведения см. в статьях [Секционированные сущности обмена сообщениями](service-bus-partitioning.md) и [Поддержка AMQP 1.0 для секционированных очередей и разделов служебной шины](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19be0-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="19be0-116">Загрузка клиентской библиотеки AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="19be0-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="19be0-117">Информацию о том, где скачать последнюю версию клиентской библиотеки Apache Qpid JMS AMQP 1.0, см. на странице [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="19be0-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="19be0-118">При построении и запуске приложений JMS с использованием служебной шины необходимо добавить следующие 4 JAR-файла из архива распространения Apache Qpid JMS AMQP 1.0 в Java CLASSPATH:</span><span class="sxs-lookup"><span data-stu-id="19be0-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="19be0-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="19be0-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="19be0-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="19be0-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="19be0-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="19be0-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="19be0-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="19be0-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="19be0-123">Создание приложений Java</span><span class="sxs-lookup"><span data-stu-id="19be0-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="19be0-124">Интерфейс JNDI</span><span class="sxs-lookup"><span data-stu-id="19be0-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="19be0-125">JMS использует интерфейс JNDI для разделения логических и физических имен.</span><span class="sxs-lookup"><span data-stu-id="19be0-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="19be0-126">С помощью JNDI разрешаются два типа объектов JMS: ConnectionFactory и Destination.</span><span class="sxs-lookup"><span data-stu-id="19be0-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="19be0-127">JNDI использует модель поставщика, к которой можно подключить различные службы каталогов для обработки заданий разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="19be0-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="19be0-128">Библиотека Apache Qpid JMS AMQP 1.0 поставляется с простым файловым поставщиком JNDI, настроенным с помощью файла свойств в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="19be0-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="19be0-129">Настройка ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="19be0-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="19be0-130">Эта запись используется для определения **ConnectionFactory** в поставщике JNDI файла свойств Qpid в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="19be0-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="19be0-131">Где **[jndi_name]** и **[ConnectionURL]** означают следующее:</span><span class="sxs-lookup"><span data-stu-id="19be0-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="19be0-132">**[jndi_name]**: логическое имя ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="19be0-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="19be0-133">Это имя, которое будет разрешено в Java-приложении с помощью метода JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="19be0-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="19be0-134">**[ConnectionURL]**: URL-адрес, предоставляющий библиотеке JMS сведения, необходимые брокеру AMQP.</span><span class="sxs-lookup"><span data-stu-id="19be0-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="19be0-135">Формат **ConnectionURL** выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="19be0-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="19be0-136">Где **[namespace]**, **[SASPolicyName]** и **[SASPolicyKey]** означают следующее:</span><span class="sxs-lookup"><span data-stu-id="19be0-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="19be0-137">**[namespace]**: пространство имен служебной шины;</span><span class="sxs-lookup"><span data-stu-id="19be0-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="19be0-138">**[SASPolicyName]**: имя политики подписанного URL-адреса;</span><span class="sxs-lookup"><span data-stu-id="19be0-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="19be0-139">**[SASPolicyKey]**: ключ политики подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="19be0-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="19be0-140">Необходимо применить URL-кодирование к паролю вручную.</span><span class="sxs-lookup"><span data-stu-id="19be0-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="19be0-141">Полезная служебная программа URL-кодирования доступна по адресу [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="19be0-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="19be0-142">Настройка назначений</span><span class="sxs-lookup"><span data-stu-id="19be0-142">Configure destinations</span></span>
<span data-ttu-id="19be0-143">Эта запись используется для определения назначения в поставщике JNDI файла свойств Qpid в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="19be0-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="19be0-144">или</span><span class="sxs-lookup"><span data-stu-id="19be0-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="19be0-145">Где **[jndi\_name]** и **[physical\_name]** означают следующее:</span><span class="sxs-lookup"><span data-stu-id="19be0-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="19be0-146">**[jndi_name]**: логическое имя назначения.</span><span class="sxs-lookup"><span data-stu-id="19be0-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="19be0-147">Это имя, которое будет разрешено в Java-приложении с помощью метода JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="19be0-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="19be0-148">**[physical_name]**: имя сущности служебной шины, которой приложение отправляет сообщения или от которого оно получает сообщения.</span><span class="sxs-lookup"><span data-stu-id="19be0-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="19be0-149">При получении данных из подписки раздела служебной шины физическое имя, указанное в JNDI, должно быть именем раздела.</span><span class="sxs-lookup"><span data-stu-id="19be0-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="19be0-150">Имя подписки предоставляется при создании устойчивой подписки в коде приложения JMS.</span><span class="sxs-lookup"><span data-stu-id="19be0-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="19be0-151">В [руководстве разработчика AMQP 1.0 для служебной шины](service-bus-amqp-dotnet.md) содержатся дополнительные сведения о работе с разделами служебной шины в JMS.</span><span class="sxs-lookup"><span data-stu-id="19be0-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="19be0-152">Написание приложения JMS</span><span class="sxs-lookup"><span data-stu-id="19be0-152">Write the JMS application</span></span>
<span data-ttu-id="19be0-153">Не существует специальных API-интерфейсов или параметров для использования JMS с Service Bus.</span><span class="sxs-lookup"><span data-stu-id="19be0-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="19be0-154">Однако существует несколько ограничений, которые будут рассмотрены ниже.</span><span class="sxs-lookup"><span data-stu-id="19be0-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="19be0-155">Как и для любого приложения JMS, первое, что необходимо — это конфигурация среды JNDI, позволяющая разрешать **ConnectionFactory** и назначения.</span><span class="sxs-lookup"><span data-stu-id="19be0-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="19be0-156">Настройка исходного контекста JNDI</span><span class="sxs-lookup"><span data-stu-id="19be0-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="19be0-157">Для настройки среды JNDI хэш-таблица со сведениями о конфигурации передаются в конструктор класса javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="19be0-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="19be0-158">Два обязательных элемента в хэш-таблице — это имя класса фабрики исходного контекста и URL-адрес поставщика.</span><span class="sxs-lookup"><span data-stu-id="19be0-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="19be0-159">В следующем примере кода показано, как настроить среду JNDI для использования поставщика JNDI на основе файла свойств Qpid с именем **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="19be0-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="19be0-160">Простое приложение JMS, использующее очередь служебной шины</span><span class="sxs-lookup"><span data-stu-id="19be0-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="19be0-161">Следующий пример программы отправляет текстовые сообщения JMS в очередь Service Bus с логическим JNDI-именем QUEUE и получает ответные сообщения.</span><span class="sxs-lookup"><span data-stu-id="19be0-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="19be0-162">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="19be0-162">Run the application</span></span>
<span data-ttu-id="19be0-163">Запущенное приложение выводит следующие данные:</span><span class="sxs-lookup"><span data-stu-id="19be0-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="19be0-164">Межплатформенный обмен сообщениями между JMS и .NET</span><span class="sxs-lookup"><span data-stu-id="19be0-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="19be0-165">В этом руководстве мы рассмотрели, как отправлять и получать сообщения Service Bus с помощью JMS.</span><span class="sxs-lookup"><span data-stu-id="19be0-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="19be0-166">Однако одно из основных преимуществ использования AMQP 1.0 состоит в том, что этот протокол позволяет приложениям, созданным из компонентов, написанных на разных языках, надежно и точно обмениваться сообщениями.</span><span class="sxs-lookup"><span data-stu-id="19be0-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="19be0-167">Используя пример приложения JMS выше и аналогичное приложение .NET, взятое из связанной статьи [Использование служебной шины на платформе .NET с протоколом AMQP 1.0](service-bus-amqp-dotnet.md), можно организовать обмен сообщениями между .NET и Java.</span><span class="sxs-lookup"><span data-stu-id="19be0-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="19be0-168">В этой статье представлены сведения о кроссплатформенном обмене сообщениями с помощью служебной шины и AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="19be0-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="19be0-169">Из JMS в .NET</span><span class="sxs-lookup"><span data-stu-id="19be0-169">JMS to .NET</span></span>
<span data-ttu-id="19be0-170">Для демонстрации отправки сообщении из JMS в .NET выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="19be0-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="19be0-171">Запустите пример приложения .NET без параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="19be0-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="19be0-172">Запустите пример приложения Java с параметром командной строки sendonly.</span><span class="sxs-lookup"><span data-stu-id="19be0-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="19be0-173">В этом режиме приложение не будет получать сообщения из очереди, оно будет только отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="19be0-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="19be0-174">В консоли приложения Java несколько раз нажмите клавишу **ВВОД**, что приведет к отправке сообщений.</span><span class="sxs-lookup"><span data-stu-id="19be0-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="19be0-175">Эти сообщения принимаются приложением .NET.</span><span class="sxs-lookup"><span data-stu-id="19be0-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="19be0-176">Вывод приложения JMS</span><span class="sxs-lookup"><span data-stu-id="19be0-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="19be0-177">Вывод приложения .NET</span><span class="sxs-lookup"><span data-stu-id="19be0-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="19be0-178">Из .NET в JMS</span><span class="sxs-lookup"><span data-stu-id="19be0-178">.NET to JMS</span></span>
<span data-ttu-id="19be0-179">Для демонстрации отправки сообщений из .NET в JMS выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="19be0-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="19be0-180">Запустите пример приложения .NET с параметром командной строки sendonly.</span><span class="sxs-lookup"><span data-stu-id="19be0-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="19be0-181">В этом режиме приложение не будет получать сообщения из очереди, оно будет только отправлять сообщения.</span><span class="sxs-lookup"><span data-stu-id="19be0-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="19be0-182">Запустите пример приложения Java без параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="19be0-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="19be0-183">В консоли приложения .NET несколько раз нажмите клавишу **ВВОД**, что приведет к отправке сообщений.</span><span class="sxs-lookup"><span data-stu-id="19be0-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="19be0-184">Эти сообщения принимаются приложением Java.</span><span class="sxs-lookup"><span data-stu-id="19be0-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="19be0-185">Вывод приложения .NET</span><span class="sxs-lookup"><span data-stu-id="19be0-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="19be0-186">Вывод приложения JMS</span><span class="sxs-lookup"><span data-stu-id="19be0-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="19be0-187">Неподдерживаемые возможности и ограничения</span><span class="sxs-lookup"><span data-stu-id="19be0-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="19be0-188">При использовании JMS по протоколу AMQP 1.0 с Service Bus действуют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="19be0-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="19be0-189">Для одного **сеанса** допускается только один **MessageProducer** или **MessageConsumer**.</span><span class="sxs-lookup"><span data-stu-id="19be0-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="19be0-190">Если требуется создать несколько **MessageProducers** или **MessageConsumers** в приложении, создайте специальный **сеанс** для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="19be0-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="19be0-191">Временные подписки раздела в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="19be0-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="19be0-192">**MessageSelectors** сейчас не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="19be0-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="19be0-193">Временные назначения, например **TemporaryQueue** и **TemporaryTopic**, сейчас не поддерживаются, как и использующие их API-интерфейсы **QueueRequestor** и **TopicRequestor**.</span><span class="sxs-lookup"><span data-stu-id="19be0-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="19be0-194">Сеансы транзакций и распределенные транзакции не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="19be0-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="19be0-195">Сводка</span><span class="sxs-lookup"><span data-stu-id="19be0-195">Summary</span></span>
<span data-ttu-id="19be0-196">В этом практическом руководстве показано использование функций обмена сообщениями, выполняемых посредством служебной шины (очередей и разделов публикации/подписки), из Java с использованием популярного JMS API и протокола AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="19be0-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="19be0-197">Протокол AMQP 1.0 Service Bus можно также использовать из других языков, в числе которых .NET, C, Python и PHP.</span><span class="sxs-lookup"><span data-stu-id="19be0-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="19be0-198">Компоненты, созданные с помощью этих языков, могут надежно и точно обмениваться сообщениями, используя AMQP 1.0 в Service Bus.</span><span class="sxs-lookup"><span data-stu-id="19be0-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19be0-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19be0-199">Next steps</span></span>
* [<span data-ttu-id="19be0-200">Поддержка AMQP 1.0 в служебной шине</span><span class="sxs-lookup"><span data-stu-id="19be0-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="19be0-201">Как использовать AMQP 1.0 с API .NET служебной шины</span><span class="sxs-lookup"><span data-stu-id="19be0-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="19be0-202">Руководство разработчика AMQP 1.0 для служебной шины</span><span class="sxs-lookup"><span data-stu-id="19be0-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="19be0-203">Начало работы с очередями служебной шины</span><span class="sxs-lookup"><span data-stu-id="19be0-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="19be0-204">Центр разработчиков Java</span><span class="sxs-lookup"><span data-stu-id="19be0-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

