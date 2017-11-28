---
title: "Отправка событий в концентраторы событий Azure с помощью C | Документация Майкрософт"
description: "Отправка событий в концентраторы событий Azure с помощью C"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="a3fcb-103">Отправка событий в концентраторы событий Azure с помощью C</span><span class="sxs-lookup"><span data-stu-id="a3fcb-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="a3fcb-104">Введение</span><span class="sxs-lookup"><span data-stu-id="a3fcb-104">Introduction</span></span>
<span data-ttu-id="a3fcb-105">Концентраторы событий — это высокомасштабируемая система, способная принимать миллионы событий в секунду, благодаря которой приложения могут обрабатывать и анализировать большие объемы данных от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a3fcb-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="a3fcb-107">Дополнительные сведения см. в [обзоре концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="a3fcb-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="a3fcb-108">В этом руководстве вы узнаете, как отправлять события в концентратор событий с помощью консольного приложения на языке C. Для получения событий выберите соответствующий язык в оглавлении слева.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="a3fcb-109">Для работы с этим учебником необходимо следующее.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="a3fcb-110">Среда разработки C.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-110">A C development environment.</span></span> <span data-ttu-id="a3fcb-111">В этом учебнике предполагается, что применяется стек gcc на виртуальной машине Azure Linux с Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="a3fcb-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="a3fcb-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-113">An active Azure account.</span></span> <span data-ttu-id="a3fcb-114">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a3fcb-115">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="a3fcb-116">Отправка сообщений в центры событий</span><span class="sxs-lookup"><span data-stu-id="a3fcb-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="a3fcb-117">В этом разделе мы напишем на языке C приложение для отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="a3fcb-118">В коде используется библиотека Proton AMQP из [проекта Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="a3fcb-119">Эта процедура аналогична использованию очередей и разделов служебной шины с AMQP на C, как показано [здесь](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="a3fcb-120">Дополнительную информацию см. в [документации по Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="a3fcb-121">Чтобы установить Qpid Proton, следуйте инструкциям для своей среды на [странице Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="a3fcb-122">Для компиляции библиотеки Proton установите следующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="a3fcb-123">Скачайте [библиотеку Qpid Proton](http://qpid.apache.org/proton/index.html) и извлеките ее, например:</span><span class="sxs-lookup"><span data-stu-id="a3fcb-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="a3fcb-124">Создайте каталог построения, скомпилируйте и установите:</span><span class="sxs-lookup"><span data-stu-id="a3fcb-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="a3fcb-125">В рабочем каталоге создайте новый файл с именем **sender.c** со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="a3fcb-126">Не забудьте заменить значения имени концентратора событий и имени пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="a3fcb-127">Также необходимо заменить версию ключа **SendRule** , закодированную как URL-адрес, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="a3fcb-128">Выполнить кодировку как URL-адрес можно [здесь](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C to stop the sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="a3fcb-129">Скомпилируйте файл при условии **gcc**:</span><span class="sxs-lookup"><span data-stu-id="a3fcb-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="a3fcb-130">В приведенном выше коде окно отправки, равное 1, используется для скорейшей принудительной отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="a3fcb-131">Обычно приложение предпримет попытку сгруппировать сообщения для увеличения пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="a3fcb-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="a3fcb-132">Информацию об использовании библиотеки Qpid Proton в этой и других средах, а также на платформах, для которых предоставляются привязки (сейчас это Perl, PHP, Python и Ruby), см. на [странице Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html).</span><span class="sxs-lookup"><span data-stu-id="a3fcb-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a3fcb-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3fcb-133">Next steps</span></span>
<span data-ttu-id="a3fcb-134">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="a3fcb-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a3fcb-135">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="a3fcb-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="a3fcb-136">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="a3fcb-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a3fcb-137">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="a3fcb-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
