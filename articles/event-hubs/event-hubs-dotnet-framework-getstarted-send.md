---
title: "aaaSend событий tooAzure концентраторов событий с помощью .NET Framework \"hello\" | Документы Microsoft"
description: "Приступить к работе, отправка событий tooEvent концентраторы, с помощью hello .NET Framework"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="8a201-103">Отправлять события tooAzure концентраторов событий, с помощью hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8a201-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="8a201-104">Введение</span><span class="sxs-lookup"><span data-stu-id="8a201-104">Introduction</span></span>

<span data-ttu-id="8a201-105">Концентраторы событий — это служба, которая обрабатывает большие объемы данных телеметрии о событиях, поступающих от подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="8a201-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="8a201-106">После сбора данных в концентраторы событий, можно хранить данные hello, с помощью кластера хранилища или преобразование с помощью поставщика аналитика в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="8a201-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="8a201-107">Эта возможность сбора и обработки крупномасштабных событий является ключевым компонентом архитектуры современных приложений, включая hello Интернета вещей (IoT).</span><span class="sxs-lookup"><span data-stu-id="8a201-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="8a201-108">В этом учебнике показано как toouse hello [портал Azure](https://portal.azure.com) toocreate концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="8a201-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="8a201-109">Здесь также показано, как с помощью консольного приложения, написанного на C# с помощью события концентратора toosend события tooan hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8a201-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="8a201-110">tooreceive события, с помощью hello .NET Framework, см. hello [получать события с помощью .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) статьи или щелкните соответствующий язык принимающей hello в левой таблице hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="8a201-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="8a201-111">toocomplete этого учебника требуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="8a201-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="8a201-112">[Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="8a201-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="8a201-113">снимки экрана приветствия в этом учебнике с помощью Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="8a201-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="8a201-114">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8a201-114">An active Azure account.</span></span> <span data-ttu-id="8a201-115">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8a201-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="8a201-116">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8a201-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="8a201-117">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="8a201-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="8a201-118">Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate в пространство имен введите концентраторов событий и получить учетные данные управления, приложение должно toocommunicate с концентратором событий hello hello.</span><span class="sxs-lookup"><span data-stu-id="8a201-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="8a201-119">toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md), продолжите hello, описанных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8a201-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="8a201-120">Создание консольного приложения отправителя</span><span class="sxs-lookup"><span data-stu-id="8a201-120">Create a sender console application</span></span>

<span data-ttu-id="8a201-121">В этом разделе вы напишете консольное приложение Windows, которое отправляет концентратора событий tooyour события.</span><span class="sxs-lookup"><span data-stu-id="8a201-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="8a201-122">В Visual Studio создайте новый проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта.</span><span class="sxs-lookup"><span data-stu-id="8a201-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="8a201-123">Имя проекта hello **отправителя**.</span><span class="sxs-lookup"><span data-stu-id="8a201-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="8a201-124">В обозревателе решений щелкните правой кнопкой мыши hello **отправителя** проекта, а затем нажмите кнопку **управление пакетами NuGet для решения**.</span><span class="sxs-lookup"><span data-stu-id="8a201-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="8a201-125">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="8a201-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="8a201-126">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="8a201-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="8a201-127">Visual Studio загрузит, устанавливает и добавляет toohello ссылки [пакет NuGet библиотеки Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="8a201-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="8a201-128">Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="8a201-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="8a201-129">Добавьте следующие поля toohello hello **программы** класс, заменив значения hello заполнитель с именем hello hello концентратора событий, созданных в предыдущем разделе hello, а строку hello соединений на уровне пространства имен, сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="8a201-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="8a201-130">Добавьте следующий метод toohello hello **программы** класса:</span><span class="sxs-lookup"><span data-stu-id="8a201-130">Add hello following method toohello **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="8a201-131">Этот метод постоянно отправляет события концентратора событий tooyour с задержкой 200 мс.</span><span class="sxs-lookup"><span data-stu-id="8a201-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="8a201-132">Наконец, добавьте следующие строки toohello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="8a201-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="8a201-133">Запустите программу hello и убедитесь, что отсутствуют ошибки.</span><span class="sxs-lookup"><span data-stu-id="8a201-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="8a201-134">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="8a201-134">Congratulations!</span></span> <span data-ttu-id="8a201-135">Теперь было отправлено концентратора событий tooan сообщений.</span><span class="sxs-lookup"><span data-stu-id="8a201-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a201-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a201-136">Next steps</span></span>
<span data-ttu-id="8a201-137">Теперь, когда вы создали рабочее приложение, которое создает концентратора событий и отправляет данные, можно переместить на toohello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="8a201-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="8a201-138">Получение событий с помощью hello узел обработчика событий</span><span class="sxs-lookup"><span data-stu-id="8a201-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="8a201-139">Справочник по узлу обработчика событий</span><span class="sxs-lookup"><span data-stu-id="8a201-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="8a201-140">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="8a201-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

