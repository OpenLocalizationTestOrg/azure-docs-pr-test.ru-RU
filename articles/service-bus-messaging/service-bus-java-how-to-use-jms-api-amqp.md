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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Как toouse hello службу сообщений Java (JMS) API с Service Bus и AMQP 1.0
Hello Advanced Message Queuing Protocol (AMQP) 1.0 — это эффективный, надежный, транспортного уровня протокол, которые можно использовать toobuild надежных кроссплатформенных приложений обмена сообщениями.

Поддержка AMQP 1.0 в шине обслуживания означает, что можно использовать hello очереди и публикации или подписки через посредника функций обмена сообщениями из диапазона различных платформ, используя эффективный двоичный протокол. Кроме того, можно создавать приложения, содержащие компоненты, созданные с использованием разнообразных языков, платформ и операционных систем.

В этой статье объясняется, как toouse Service Bus функций обмена сообщениями (очередей и публикации или подписки разделов) из приложений Java с помощью hello популярных службу сообщений Java (JMS) стандартный API. Отсутствует [сопутствующая статья](service-bus-amqp-dotnet.md) , объясняется, как toodo hello же с помощью hello API .NET служебной шины. Можно использовать эти два руководства по вместе toolearn, об обмене сообщениями между различными платформами, с помощью AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Приступая к работе со служебной шиной
В этом руководстве предполагается, что вы уже создали пространство имен служебной шины, содержащее очередь с именем **queue1**. Если этого не сделать, то вы можете [создать пространство имен hello и очереди](service-bus-create-namespace-portal.md) с помощью hello [портал Azure](https://portal.azure.com). Дополнительные сведения о том, как отображается toocreate пространства имен служебной шины и очереди, [приступить к работе с очередями Service Bus](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Секционированные очереди и разделы также поддерживают AMQP. Дополнительные сведения см. в статьях [Секционированные сущности обмена сообщениями](service-bus-partitioning.md) и [Поддержка AMQP 1.0 для секционированных очередей и разделов служебной шины](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Загрузка клиентской библиотеки AMQP 1.0 JMS hello
Сведения о котором toodownload hello последнюю версию клиентской библиотеки Apache Qpid JMS AMQP 1.0 hello [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Необходимо добавить следующие четыре JAR-файла из toohello архива распространения Apache Qpid JMS AMQP 1.0 hello Java CLASSPATH при построении и запуске приложений JMS с Service Bus hello:

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Создание приложений Java
### <a name="java-naming-and-directory-interface-jndi"></a>Интерфейс JNDI
JMS использует hello именования Java и каталог интерфейс JNDI toocreate разделение логических и физических имен. С помощью JNDI разрешаются два типа объектов JMS: ConnectionFactory и Destination. JNDI использует модель поставщика, в которую можно подключить разрешения имен установки toohandle служб другой каталог. Hello Apache Qpid JMS AMQP 1.0 библиотеки поставляется с простых свойств файловых JNDI поставщика, который настраивается с помощью файла свойств hello следующий формат:

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

#### <a name="configure-hello-connectionfactory"></a>Настройка hello ConnectionFactory
Здравствуйте записи, используемой toodefine **ConnectionFactory** в hello Qpid JNDI поставщик свойств файла имеет hello следующий формат:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Где **[jndi_name]** и **[ConnectionURL]** имеют hello следующие значения:

* **[jndi_name]** : hello логическое имя hello ConnectionFactory. Это имя hello, который будет разрешен в hello приложения Java, с помощью метода JNDI IntialContext.lookup() hello.
* **[ConnectionURL]** : URL-адрес, предоставляющий библиотеке JMS hello сведениями hello необходимые toohello брокера AMQP.

Формат Hello hello **ConnectionURL** выглядит следующим образом:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Где **[пространство имен]**, **[SASPolicyName]** и **[SASPolicyKey]** имеют hello следующие значения:

* **[пространство имен]** : hello пространства имен Service Bus.
* **[SASPolicyName]** : hello имя политики очереди подписи общего доступа.
* **[SASPolicyKey]** : hello ключ политики очереди подписи общего доступа.

> [!NOTE]
> URL-кодирование пароля hello необходимо вручную. Полезная служебная программа URL-кодирования доступна по адресу [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Настройка назначений
Здравствуйте, toodefine запись, используемая для копирования в поставщик JNDI файла свойств Qpid hello данных является hello следующая формата:

```
queue.[jndi_name] = [physical_name]
```

или

```
topic.[jndi_name] = [physical_name]
```

Где **[jndi\_имя]** и **[физического\_имя]** имеют hello следующие значения:

* **[jndi_name]** : hello логическое имя назначения «hello». Это имя hello, который будет разрешен в hello приложения Java, с помощью метода JNDI IntialContext.lookup() hello.
* **[physical_name]** : имя hello hello приложения hello toowhich сущности служебной шины отправлять или получать сообщения.

> [!NOTE]
> При получении из подписки раздела Service Bus hello физическое имя, указанное в JNDI следует hello имя раздела hello. имя подписки Hello предоставляется при создании устойчивой подписки hello в коде приложения JMS hello. Hello [Service Bus AMQP 1.0 руководство разработчика](service-bus-amqp-dotnet.md) содержатся дополнительные сведения о работе с разделы служебной шины из JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Написать приложение hello JMS
Не существует специальных API-интерфейсов или параметров для использования JMS с Service Bus. Однако существует несколько ограничений, которые будут рассмотрены ниже. Как и любого приложения JMS hello первое, что необходимые конфигурации среды JNDI hello, может tooresolve toobe **ConnectionFactory** и назначения.

#### <a name="configure-hello-jndi-initialcontext"></a>Настройка hello JNDI InitialContext
Hello среды JNDI настраивается путем передачи хэш-таблицу сведений о конфигурации в конструктор hello класса javax.naming.InitialContext hello. Hello двумя обязательными элементами в хэш-таблице hello: имя класса hello hello начальной фабрики контекста и hello URL-адрес поставщика. Hello следующий код показывает, как tooconfigure hello JNDI toouse hello Qpid свойства файла среды на основе поставщика JNDI с свойства файл с именем **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Простое приложение JMS, использующее очередь служебной шины
Hello следующий пример программы очереди Service Bus tooa JMS TextMessages с hello JNDI логическое имя очереди, отправляет и получает сообщения hello обратно.

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

### <a name="run-hello-application"></a>Запустите приложение hello
Запуск приложения hello выводятся данные hello формы:

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

## <a name="cross-platform-messaging-between-jms-and-net"></a>Межплатформенный обмен сообщениями между JMS и .NET
В этом руководстве показано, как toosend и получать сообщения tooand с Service Bus с помощью JMS. Одним из ключевых преимуществ hello AMQP 1.0 то, что позволяет приложениям toobe, построенная для компонентов, написанных на разных языках с сообщения, которыми обмениваются надежно и с полной точностью.

С помощью JMS hello демонстрационного приложения, описанного выше и аналогичные приложения .NET, взяты из сопутствующая статья [с использованием служебной шины из .NET с AMQP 1.0](service-bus-amqp-dotnet.md), обмен сообщениями между .NET и Java. Эта статья Дополнительные сведения о hello кросс платформенных обмена сообщениями с использованием Service Bus и AMQP 1.0.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET обмена сообщениями:

* Запустите приложение образец hello .NET без аргументов командной строки.
* Запустите образец приложения Java hello с аргументом командной строки «sendonly» hello. В этом режиме hello приложения не будут получать сообщения из очереди hello, он будет отправлять.
* Нажмите клавишу **ввод** несколько раз в консоли приложения hello Java, которое может вызвать toobe сообщения отправляются.
* Эти сообщения принимаются hello приложения .NET.

#### <a name="output-from-jms-application"></a>Вывод приложения JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Вывод приложения .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>.NET tooJMS
tooJMS .NET toodemonstrate обмена сообщениями:

* Запустите пример приложения hello .NET с помощью аргумента командной строки «sendonly» hello. В этом режиме hello приложения не будут получать сообщения из очереди hello, он будет отправлять.
* Запустите приложение образец hello Java без аргументов командной строки.
* Нажмите клавишу **ввод** несколько раз в консоли приложения hello .NET, что приведет к toobe сообщения отправляются.
* Эти сообщения принимаются hello приложения Java.

#### <a name="output-from-net-application"></a>Вывод приложения .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Вывод приложения JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Неподдерживаемые возможности и ограничения
При использовании JMS через протокол AMQP 1.0 с Service Bus, а именно существуют Hello следующие ограничения:

* Для одного **сеанса** допускается только один **MessageProducer** или **MessageConsumer**. Если вам требуется toocreate несколько **MessageProducers** или **MessageConsumers** в приложении, создать выделенную **сеанса** для каждого из них.
* Временные подписки раздела в настоящее время не поддерживаются.
* **MessageSelectors** сейчас не поддерживаются.
* Временные назначения; например **TemporaryQueue**, **TemporaryTopic** не поддерживаются в настоящее время, а также hello **QueueRequestor** и **TopicRequestor**API, использовать их.
* Сеансы транзакций и распределенные транзакции не поддерживаются.

## <a name="summary"></a>Сводка
Это как tooguide было показано, как toouse через посредника Service Bus функций обмена сообщениями (очередей и публикации или подписки разделов) с помощью Java hello популярные API JMS и AMQP 1.0.

Протокол AMQP 1.0 Service Bus можно также использовать из других языков, в числе которых .NET, C, Python и PHP. Компоненты, созданные с помощью этих разных языков могут обмениваться сообщениями надежно и с полной точностью, с помощью поддержки hello AMQP 1.0 в шине обслуживания.

## <a name="next-steps"></a>Дальнейшие действия
* [Поддержка AMQP 1.0 в служебной шине](service-bus-amqp-overview.md)
* [Как toouse AMQP 1.0 с hello API .NET служебной шины](service-bus-dotnet-advanced-message-queuing.md)
* [Руководство разработчика AMQP 1.0 для служебной шины](service-bus-amqp-dotnet.md)
* [Начало работы с очередями служебной шины](service-bus-dotnet-get-started-with-queues.md)
* [Центр разработчиков Java](https://azure.microsoft.com/develop/java/)

