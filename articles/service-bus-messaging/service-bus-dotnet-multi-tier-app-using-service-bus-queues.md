---
title: "aaa.NET многоуровневого приложения с помощью Azure Service Bus | Документы Microsoft"
description: "Учебник .NET, в котором помогает разрабатывать приложения для многоуровневых приложений в Azure, которая использует toocommunicate очереди Service Bus между уровнями."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Многоуровневое приложение .NET, использующее очереди служебной шины Azure
## <a name="introduction"></a>Введение
Разработка для Microsoft Azure — это простой, с помощью Visual Studio и hello бесплатные Azure SDK для .NET. Этот учебник поможет выполнить шаги toocreate hello приложения, использующего несколько ресурсов Azure, работающих в локальной среде.

Вы узнаете следующее hello.

* Как tooenable компьютера для разработки Azure с одним загрузить и установить.
* Как toouse toodevelop Visual Studio для Azure.
* Как toocreate многоуровневого приложения в Azure с помощью веб- и рабочих ролей.
* Как toocommunicate между уровнями с использованием очередей Service Bus.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

В этом учебнике предстоит Постройте и запустите многоуровневого приложения hello в облачной службе Azure. Hello внешнего интерфейса веб-роль ASP.NET MVC. она hello серверной части рабочих роль, которая использует очереди Service Bus. Можно создать hello того же многоуровневые приложения с внешнего интерфейса hello как веб-проекта, развернутого tooan вместо облачной службы веб-сайте Azure. Также можно попробовать hello [на локальная/облачная гибридного приложения .NET](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) учебника.

Hello следующем снимке экрана показано приложение hello завершена.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Обзор сценария: обмен данными между ролями
toosubmit заказ для обработки переднего плана пользовательского интерфейса компонента hello, работающих в веб-роли hello, должны взаимодействовать с логикой hello среднего уровня, работающих в hello рабочей роли. В этом примере для hello взаимодействия между уровнями hello сообщений Service Bus.

С помощью Service Bus обмен сообщениями между средней уровни hello web и разделяет эти два компонента. В отличие от hello toodirect обмена сообщениями (то есть, TCP или HTTP), веб-уровень не напрямую; подключиться toohello среднего уровня Вместо этого он отправляет рабочих единиц, как сообщения, в Service Bus, который надежно сохраняет их, пока не будет готов tooconsume hello среднего уровня и обрабатывать их.

Шина обслуживания предоставляет два сообщениями через посредника toosupport сущностей: очереди и разделы. С очередями каждое сообщение отправлено toohello очереди используется один получатель. Разделы поддерживать шаблон публикации или подписки hello, в котором каждое опубликованное сообщение становится доступной tooa подписки, зарегистрированной разделе hello. Для каждой подписки ведется собственная логическая очередь сообщений. Подписки также могут быть настроены правила фильтрации, которые ограничивают набор hello сообщений передан toothose очереди подписки hello, соответствующих фильтру hello. Hello следующий пример использует очереди Service Bus.

![][1]

По сравнению с прямым обменом сообщениями этот механизм взаимодействия имеет ряд преимуществ.

* **Временное разделение.** С hello шаблоном асинхронного обмена сообщениями, производители и потребители не должны быть в Интернете в hello то же время. Service Bus надежно хранит сообщения, пока сторона потребителя hello не будет готова к приему. Это позволяет hello компоненты hello распределенного приложения toobe отключен, либо добровольно, например, для обслуживания или из-за сбоя компонента tooa без ущерба для системы в целом. Кроме того использование приложения hello безопасности может потребоваться toocome сети только в определенное время дня hello.
* **Выравнивание нагрузки.** Во многих приложениях системная нагрузка изменяется во времени, во время обработки hello время, необходимое для каждой единицы работы, как правило, постоянно. Посредничество отправителями и получателями сообщений с очередью означает, что этот hello использует только toobe потребностей приложения (hello рабочих процессов) подготовить tooaccommodate среднюю нагрузку вместо пиковой нагрузки. Глубина Hello hello очереди будет расти или уменьшаться как hello входящая нагрузка меняется. Это напрямую экономит деньги с точки зрения hello объема нагрузки приложения hello необходимые tooservice инфраструктуры.
* **Балансировка нагрузки.** По мере увеличения нагрузки больше рабочих процессов могут добавляться tooread из очереди hello. Каждое сообщение обрабатывается только один hello рабочих процессов. Кроме того этот запросу распределения нагрузки с учетом позволяет оптимального использования hello рабочих машин даже в случае различаются машины работника с точки зрения вычислительной мощности, как они будут опрашивать сообщения на максимальной скорости. Данный шаблон часто называется hello *конкурентной* шаблон.
  
  ![][2]

Hello в следующих разделах рассматриваются hello код, который реализует этой архитектуре.

## <a name="set-up-hello-development-environment"></a>Настройка среды разработки hello
Прежде чем начать, разработке приложений Azure, средства hello и настройка среды разработки.

1. Установить hello Azure SDK для .NET из пакета SDK для hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. В hello **.NET** столбец, выберите версию hello [Visual Studio](http://www.visualstudio.com) вы используете. Hello шаги в данном руководстве используйте Visual Studio 2015, но они также работают с Visual Studio 2017 г.
3. При запросе toorun или сохранить hello установщика нажмите **запуска**.
4. В hello **Web Platform Installer**, нажмите кнопку **установить** и продолжите установку hello.
5. После завершения установки hello, будет иметь все необходимые toostart приложение hello toodevelop. Hello SDK содержит средства, позволяющие легко разрабатывать приложения Azure в Visual Studio.

## <a name="create-a-namespace"></a>Создание пространства имен
Hello следующим шагом является toocreate пространства имен службы и получить ключ подписи общего доступа (SAS). Пространство имен определяет границы каждого приложения, предоставляемого через служебную шину. Ключ SAS создается системой hello при создании пространства имен. Hello сочетание пространства имен и ключ SAS предоставляет учетные данные hello для приложения tooan access tooauthenticate Service Bus.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Создание веб-роли
В этом разделе сборки hello интерфейсной части приложения. Сначала необходимо создать страницы приветствия, приложение отображает.
После этого добавьте код, который отправляет очередь Service Bus tooa элементов и отображает сведения о состоянии очереди hello.

### <a name="create-hello-project"></a>Создание проекта hello
1. С правами доступа администратора, запустите Visual Studio: щелкните правой кнопкой мыши hello **Visual Studio** значок программы, а затем нажмите кнопку **Запуск от имени администратора**. Эмулятор вычислений Azure Hello, описанных далее в этой статье, требует запуска Visual Studio с правами администратора.
   
   В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.
2. В разделе **Установленные шаблоны** области **Visual C#** щелкните **Облако**, а затем — **Облачная служба Azure**. Имя проекта hello **MultiTierApp**. Нажмите кнопку **ОК**.
   
   ![][9]
3. В списке ролей **.NET Framework 4.5** дважды щелкните **Веб-роль ASP.NET**.
   
   ![][10]
4. Наведите указатель мыши на **WebRole1** под **решение облачной службы Azure**, щелкните значок карандаша hello и переименования hello веб-роли слишком**FrontendWebRole**. Нажмите кнопку **ОК**. (Обратите внимание на написание слова «Frontend» со строчной буквой «e» — не «FrontEnd».)
   
   ![][11]
5. Из hello **новый проект ASP.NET** диалогового окна hello **выберите шаблон** выберите **MVC**.
   
   ![][12]
6. По-прежнему в hello **новый проект ASP.NET** диалогового окна выберите hello **изменить аутентификацию** кнопки. В hello **изменить аутентификацию** диалоговое окно, нажмите кнопку **без проверки подлинности**, а затем нажмите кнопку **ОК**. В этом учебнике выполняется развертывание приложения, для которого не требуется имя пользователя.
   
    ![][16]
7. Вернитесь в hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **ОК** toocreate hello проекта.
8. В **обозревателе решений**, в hello **FrontendWebRole** щелкните правой кнопкой мыши проект **ссылки**, нажмите кнопку **управление пакетами NuGet**.
9. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Выберите hello **WindowsAzure.ServiceBus** пакет, нажмите кнопку **установить**и примите условия использования hello.
   
   ![][13]
   
   Обратите внимание, что hello необходимые теперь существуют ссылки на сборки клиента и были добавлены некоторые новые файлы кода.
10. В **обозревателе решений** щелкните правой кнопкой мыши **Модели**, а затем выберите **Добавить** и **Класс**. В hello **имя** hello введите имя **OnlineOrder.cs**. Нажмите кнопку **Добавить**.

### <a name="write-hello-code-for-your-web-role"></a>Написание кода hello для веб-роли
В этом разделе создается hello различным страницам, отображаемых в приложении.

1. Замените существующее определение пространства имен в файле OnlineOrder.cs hello в Visual Studio, hello, следующий код:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. В **обозревателе решений** дважды щелкните **Controllers\HomeController.cs**. Добавьте следующее hello **с помощью** инструкции вверху hello hello файл hello tooinclude пространства имен для модели, который вы только что создали, а также Service Bus.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Также в файл HomeController.cs hello в Visual Studio, замените существующее определение пространства имен после кода hello. Этот код содержит методы для обработки hello отправки элементов очереди toohello.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Из hello **построения** меню, нажмите кнопку **построить решение** tootest hello правильность выполненной работы к текущему моменту.
5. Теперь создайте представление hello для hello `Submit()` метода, созданного ранее. Щелкните правой кнопкой мыши в пределах hello `Submit()` метод (hello перегрузку `Submit()` , не принимает параметров) и выберите **добавить представление**.
   
   ![][14]
6. Диалоговое окно для создания представления hello. В hello **шаблона** выберите **создать**. В hello **класс модели** выберите hello **OnlineOrder** класса.
   
   ![][15]
7. Щелкните **Добавить**.
8. Теперь изменим hello отображается имя приложения. В **обозревателе решений**, дважды щелкните **представления\общие\\_Layout.cshtml** файл tooopen его в редакторе Visual Studio hello.
9. Замените все вхождения элемента **Мое приложение ASP.NET** текстом **Продукты LITWARE**.
10. Удалите hello **Главная**, **о**, и **контакт** ссылки. Удаление выделенной hello кода:
    
    ![][28]
11. Наконец измените hello отправки страницы tooinclude некоторые сведения об очереди hello. В **обозревателе решений**, дважды щелкните **Views\Home\Submit.cshtml** файл tooopen его в редакторе Visual Studio hello. Добавьте следующие строки после hello `<h2>Submit</h2>`. Теперь, hello `ViewBag.MessageCount` пуст. Вы заполните его позже.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Пользовательский интерфейс реализован. Можно нажать клавишу **F5** toorun приложения и убедитесь, что он выглядит так, как ожидалось.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Написание кода hello для отправки в очередь Service Bus tooa элементов
Теперь добавьте код для отправки в очередь tooa элементов. Сначала вам нужно создать класс, содержащий информацию о подключении к очереди служебной шины, а затем — инициализировать подключение из Global.aspx.cs. И, наконец обновите код отправки hello, созданный ранее в tooa HomeController.cs tooactually отправки элементов очереди Service Bus.

1. В **обозревателе решений**, щелкните правой кнопкой мыши **FrontendWebRole** (щелкните правой кнопкой мыши проект hello, не hello роли). Щелкните **Добавить** и **Класс**.
2. Имя класса hello **QueueConnector.cs**. Нажмите кнопку **добавить** toocreate hello класса.
3. Теперь добавьте код, который инкапсулирует сведения о соединении hello и инициализирует очереди Service Bus tooa hello. Замените все содержимое hello QueueConnector.cs после кода hello и введите значения для `your Service Bus namespace` (ваше пространство имен) и `yourKey`, который является hello **первичного ключа** ранее получены из hello Azure портал.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Теперь нужно обеспечить вызов метода **Initialize**. В **обозревателе решений** дважды щелкните **Global.asax\Global.asax.cs**.
5. Добавьте следующие строки кода в конце hello hello hello **Application_Start** метод.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Наконец обновите hello веб-кода, созданного ранее, для отправки в очередь toohello элементов. В **обозревателе решений** дважды щелкните **Controllers\HomeController.cs**.
7. Обновление hello `Submit()` метод (hello перегрузку, которая не принимает параметров) следующим tooget приветственное сообщение для расчета hello очереди.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Обновление hello `Submit(OnlineOrder order)` метод (hello перегрузку, которая принимает один параметр) следующим toosubmit порядок сведения toohello очереди.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Теперь можно запустить приложение hello еще раз. Каждый раз при отправке заказа, увеличивает число сообщений hello.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Создание рабочей роли hello
Теперь вы создадите hello рабочая роль, обрабатывающая hello отправки заказа. В этом примере используется hello **рабочая роль с очередью Service Bus** шаблон проекта Visual Studio. Hello необходимые учетные данные уже получен из портала hello.

1. Убедитесь, что вы подключились Visual Studio tooyour учетная запись Azure.
2. В Visual Studio в **обозревателе решений** щелкните правой кнопкой мыши **ролей** папку hello **MultiTierApp** проекта.
3. Щелкните **Добавить** и выберите **Создать проект рабочей роли**. Hello **добавить новый проект роли** откроется диалоговое окно.
   
   ![][26]
4. В hello **добавить новый проект роли** диалоговое окно, нажмите кнопку **рабочая роль с очередью Service Bus**.
   
   ![][23]
5. В hello **имя** поле, имя проекта hello **OrderProcessingRole**. Нажмите кнопку **Добавить**.
6. Скопируйте строку подключения hello, полученный на шаге 9 буфера toohello раздел «Создать пространство имен служебной шины» hello.
7. В **обозревателе решений**, щелкните правой кнопкой мыши hello **OrderProcessingRole** созданный на шаге 5 (Убедитесь, что вы щелкните правой кнопкой мыши **OrderProcessingRole** под **Роли**, а не hello класса). Выберите пункт **Свойства**.
8. На hello **параметры** вкладка hello **свойства** диалоговое окно, щелкните внутри hello **значение** поле для **Microsoft.ServiceBus.ConnectionString**, а затем вставьте значение конечной точки hello, скопированным на шаге 6.
   
   ![][25]
9. Создание **OnlineOrder** класса toorepresent hello заказов, как обработать их из очереди hello. При необходимости используйте ранее созданный класс. В **обозревателе решений**, щелкните правой кнопкой мыши hello **OrderProcessingRole** класса (щелкните правой кнопкой мыши значок класса hello, не hello роли). Щелкните **Добавить**, а затем — **Существующий элемент**.
10. Найдите вложенную папку toohello для **FrontendWebRole\Models**, а затем дважды щелкните **OnlineOrder.cs** tooadd его toothis проекта.
11. В **WorkerRole.cs**, измените значение hello hello **QueueName** переменную `"ProcessingQueue"` слишком`"OrdersQueue"` как показано в следующим hello.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Добавьте следующее hello using с hello начало файла WorkerRole.cs hello.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. В hello `Run()` функция внутри hello `OnMessage()` call, замените содержимое hello hello `try` предложение with hello, следующий код.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Вы завершили приложения hello. Полный приложения hello можно проверить, щелкнув правой кнопкой мыши проект MultiTierApp hello в обозревателе решений при выборе **Назначить запускаемым проектом**, а затем нажать клавишу F5. Обратите внимание, что количество сообщений не увеличивается, так как hello рабочая роль обрабатывает элементы из очереди hello и помечает их как выполненные. Выходные данные трассировки hello рабочей роли можно увидеть, просмотрев hello пользовательский Интерфейс эмулятора вычислений Azure. Это можно сделать, щелкнув правой кнопкой мыши значок эмулятора hello в hello области уведомлений панели задач и выбрав **Показать пользовательский Интерфейс эмулятора вычислений**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о Service Bus см. следующие ресурсы hello.  

* [Документация по служебной шине Azure][sbdocs]  
* [Страница службы служебной шины][sbacom]  
* [Как tooUse очереди шины обслуживания][sbacomqhowto]  

toolearn Дополнительные сведения о многоуровневые сценарии, см.:  

* [Многоуровневое приложение .NET, использующее таблицы, очереди и большие двоичные объекты хранилища][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
