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
# <a name="send-events-tooazure-event-hubs-using-java"></a>Отправлять события tooAzure концентраторов событий, с помощью Java

## <a name="introduction"></a>Введение
Концентраторы событий — это система высокой степенью масштабирования приема, можно принять миллионов событий в секунду, включение tooprocess приложения и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений. После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.

Дополнительные сведения см. в разделе hello [Обзор концентраторов событий][Event Hubs overview].

В этом учебнике показано как концентратора событий tooan toosend событий с помощью консольного приложения на языке Java. tooreceive события с помощью библиотеки hello узел обработчика событий Java, см. [в этой статье](event-hubs-java-get-started-receive-eph.md), или выберите соответствующий язык принимающей hello в левой таблице hello содержимого.

В порядке toocomplete этого учебника требуется hello следующие:

* Среда разработки Java. Для этого руководства предполагается использование среды [Eclipse](https://www.eclipse.org/).
* Активная учетная запись Azure. <br/>Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Бесплатная пробная версия Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Отправка сообщений tooEvent концентраторы
Hello клиентской библиотеки Java для концентраторов событий доступна для использования в проектах Maven из hello [Maven центральный репозиторий](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Вы можете обратиться к этой библиотеке, с помощью объявления зависимостей в файле проекта Maven hello.    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Для различных типов среды сборки c, можно явно загрузить файлы JAR hello последнего выпуска из hello [Maven центральный репозиторий](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Для простых событий издателя импортировать hello *com.microsoft.azure.eventhubs* пакет для клиентских классов hello концентраторов событий и hello *com.microsoft.azure.servicebus* пакета программа классов, например как общие исключения, которые являются общими с клиентом обмена сообщениями Azure Service Bus hello. 

Для следующих образец hello сначала необходимо создайте новый проект Maven для приложений консоли или оболочки в избранные среда разработки Java. Имя класса hello `Send`.     

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

Замените имена hub hello пространства имен и событие hello значения, используемые при создании концентратора событий hello.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Затем создайте одиночное событие, преобразовав строку в байтовую кодировку UTF-8. Затем создайте новый экземпляр клиента концентраторов событий из строки подключения hello и отправить сообщение hello.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Получение событий с помощью hello EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Обзор концентраторов событий Azure][Event Hubs overview].
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md