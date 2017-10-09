---
title: "tooAzure aaaSend событий концентраторов событий с помощью C | Документы Microsoft"
description: "Отправлять события tooAzure концентраторов событий, с помощью C"
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
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="69629-103">Отправлять события tooAzure концентраторов событий, с помощью C</span><span class="sxs-lookup"><span data-stu-id="69629-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="69629-104">Введение</span><span class="sxs-lookup"><span data-stu-id="69629-104">Introduction</span></span>
<span data-ttu-id="69629-105">Концентраторы событий — это система высокой степенью масштабирования приема, можно принять миллионов событий в секунду, включение tooprocess приложения и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="69629-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="69629-106">После сбора данных в концентраторах событий их можно преобразовать и сохранить с помощью любого поставщика аналитики в реальном времени или в кластере хранилища.</span><span class="sxs-lookup"><span data-stu-id="69629-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="69629-107">Дополнительные сведения см. в разделе hello [Обзор концентраторов событий] [Обзор концентраторов событий].</span><span class="sxs-lookup"><span data-stu-id="69629-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="69629-108">В этом учебнике вы узнаете, как toosend события tooan события концентратора с помощью консольного приложения в событиях C. tooreceive hello соответствующие принимающей в выберите язык hello левой оглавление.</span><span class="sxs-lookup"><span data-stu-id="69629-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="69629-109">toocomplete этого учебника вам потребуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="69629-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="69629-110">Среда разработки C.</span><span class="sxs-lookup"><span data-stu-id="69629-110">A C development environment.</span></span> <span data-ttu-id="69629-111">В этом учебнике предполагается hello gcc стека на виртуальной Машине Linux Azure с Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="69629-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="69629-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="69629-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="69629-113">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="69629-113">An active Azure account.</span></span> <span data-ttu-id="69629-114">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="69629-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="69629-115">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69629-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="69629-116">Отправка сообщений tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="69629-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="69629-117">В этом разделе мы записи концентратора событий tooyour C приложения toosend события.</span><span class="sxs-lookup"><span data-stu-id="69629-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="69629-118">Hello код использует библиотеку Proton AMQP hello из hello [проекта Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="69629-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="69629-119">Это является аналогом toousing Service Bus очереди и разделы с помощью AMQP от C, как показано [здесь](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="69629-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="69629-120">Дополнительную информацию см. в [документации по Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="69629-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="69629-121">Из hello [Qpid AMQP Messenger страницу](https://qpid.apache.org/proton/messenger.html), следуйте инструкциям hello tooinstall Qpid Proton, в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="69629-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="69629-122">toocompile hello библиотеки Proton, установите hello следующие пакеты:</span><span class="sxs-lookup"><span data-stu-id="69629-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="69629-123">Загрузите hello [Qpid Proton библиотеки](http://qpid.apache.org/proton/index.html)и извлеките его, например:</span><span class="sxs-lookup"><span data-stu-id="69629-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="69629-124">Создайте каталог построения, скомпилируйте и установите:</span><span class="sxs-lookup"><span data-stu-id="69629-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="69629-125">В рабочий каталог, создайте новый файл с именем **sender.c** с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="69629-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="69629-126">Не забывайте toosubstitute hello значение для имени концентратора событий и пространства имен.</span><span class="sxs-lookup"><span data-stu-id="69629-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="69629-127">Кроме того, необходимо заменить URL-закодированной версией hello ключа для hello **SendRule** созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="69629-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="69629-128">Выполнить кодировку как URL-адрес можно [здесь](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="69629-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
        printf("Press Ctrl-C toostop hello sender process\n");
   
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
6. <span data-ttu-id="69629-129">Скомпилируйте файл hello, при условии, что **gcc**:</span><span class="sxs-lookup"><span data-stu-id="69629-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="69629-130">В этом коде мы используем исходящих окна 1 сообщение hello tooforce ожидания как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="69629-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="69629-131">В общем случае приложения следует проверить пропускную способность tooincrease сообщения toobatch.</span><span class="sxs-lookup"><span data-stu-id="69629-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="69629-132">. В разделе hello [Qpid AMQP Messenger страницы](https://qpid.apache.org/proton/messenger.html) сведения о как toouse hello Qpid Proton библиотеки в этом и других средах, а также от платформы, для которых предоставляются привязки (в настоящее время Perl, PHP, Python и Ruby).</span><span class="sxs-lookup"><span data-stu-id="69629-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="69629-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69629-133">Next steps</span></span>
<span data-ttu-id="69629-134">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="69629-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="69629-135">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="69629-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="69629-136">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="69629-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="69629-137">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="69629-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
