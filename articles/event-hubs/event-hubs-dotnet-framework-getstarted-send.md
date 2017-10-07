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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Отправлять события tooAzure концентраторов событий, с помощью hello .NET Framework

## <a name="introduction"></a>Введение

Концентраторы событий — это служба, которая обрабатывает большие объемы данных телеметрии о событиях, поступающих от подключенных устройств и приложений. После сбора данных в концентраторы событий, можно хранить данные hello, с помощью кластера хранилища или преобразование с помощью поставщика аналитика в реальном времени. Эта возможность сбора и обработки крупномасштабных событий является ключевым компонентом архитектуры современных приложений, включая hello Интернета вещей (IoT).

В этом учебнике показано как toouse hello [портал Azure](https://portal.azure.com) toocreate концентратора событий. Здесь также показано, как с помощью консольного приложения, написанного на C# с помощью события концентратора toosend события tooan hello .NET Framework. tooreceive события, с помощью hello .NET Framework, см. hello [получать события с помощью .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) статьи или щелкните соответствующий язык принимающей hello в левой таблице hello содержимого.

toocomplete этого учебника требуется hello следующие предварительные требования:

* [Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com). снимки экрана приветствия в этом учебнике с помощью Visual Studio 2017 г.
* Активная учетная запись Azure. Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Создание пространства имен концентраторов событий и концентратора событий

Hello первым шагом является toouse hello [портал Azure](https://portal.azure.com) toocreate в пространство имен введите концентраторов событий и получить учетные данные управления, приложение должно toocommunicate с концентратором событий hello hello. toocreate пространство имен и концентратора событий, выполните процедуру hello в [в этой статье](event-hubs-create.md), продолжите hello, описанных в этом учебнике.

## <a name="create-a-sender-console-application"></a>Создание консольного приложения отправителя

В этом разделе вы напишете консольное приложение Windows, которое отправляет концентратора событий tooyour события.

1. В Visual Studio создайте новый проект приложения рабочего стола Visual C# с помощью hello **консольное приложение** шаблона проекта. Имя проекта hello **отправителя**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. В обозревателе решений щелкните правой кнопкой мыши hello **отправителя** проекта, а затем нажмите кнопку **управление пакетами NuGet для решения**. 
3. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Нажмите кнопку **установить**и примите условия использования hello. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio загрузит, устанавливает и добавляет toohello ссылки [пакет NuGet библиотеки Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Добавьте следующее hello `using` инструкции вверху hello hello **Program.cs** файла:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Добавьте следующие поля toohello hello **программы** класс, заменив значения hello заполнитель с именем hello hello концентратора событий, созданных в предыдущем разделе hello, а строку hello соединений на уровне пространства имен, сохраненный ранее.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Добавьте следующий метод toohello hello **программы** класса:
   
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
   
  Этот метод постоянно отправляет события концентратора событий tooyour с задержкой 200 мс.
7. Наконец, добавьте следующие строки toohello hello **Main** метод:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Запустите программу hello и убедитесь, что отсутствуют ошибки.
  
Поздравляем! Теперь было отправлено концентратора событий tooan сообщений.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы создали рабочее приложение, которое создает концентратора событий и отправляет данные, можно переместить на toohello следующие сценарии:

* [Получение событий с помощью hello узел обработчика событий](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Справочник по узлу обработчика событий](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

