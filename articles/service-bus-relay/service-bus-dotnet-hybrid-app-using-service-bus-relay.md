---
title: "aaaAzure ретрансляции WCF гибридного на локальные и облачные приложения (.NET) | Документы Microsoft"
description: "Узнайте, как toocreate .NET на локальная/облачная гибридного приложения с помощью ретрансляции WCF в Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Создание локального или облачного гибридного приложения .NET с использованием ретранслятора WCF Azure
## <a name="introduction"></a>Введение

В этой статье показано, как toobuild гибридной облачные приложения с Microsoft Azure и Visual Studio. Hello учебнике предполагается, что у вас есть нет опыта работы с Azure. Менее чем за 30 минут будет иметь приложение, которое использует несколько ресурсов Azure и работающих в облаке hello.

Вы узнаете:

* Как toocreate или адаптировать существующей веб-службы, для использования с веб-решений.
* Как toouse hello Azure WCF ретрансляции tooshare данных между приложением Azure и веб-служба размещается в другом месте.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Как ретранслятор Azure помогает работать с гибридными решениями

Бизнес-решения обычно состоят из сочетание пользовательским кодом, написанным tootackle новый и уникальные бизнес-требований и существующие функциональные возможности, предоставляемые решения и систем, которые уже находятся на месте.

Архитекторам решений запускаются облачные hello toouse для упрощения обработки требований масштабирования и снизить эксплуатационные затраты. При этом можно найти что существующие ресурсы службы, они бы хотели tooleverage строительными блоками для своих решений являются корпоративным брандмауэром hello и из легко охватить для доступа, hello облачного решения. Многие внутренних служб не строятся или размещенных таким образом, они могут быть легко предоставлены на краю корпоративной сети hello.

[Azure ретрансляции](https://azure.microsoft.com/services/service-bus/) предназначен для hello вариант использования принятия существующих веб-служб Windows Communication Foundation (WCF) и внесения тех служб toosolutions получить безопасный доступ, которые находятся за пределами корпоративной сети hello без необходимости Инфраструктура корпоративной сети toohello влияние изменений. Такие службы ретрансляции по-прежнему размещены внутри существующей средой, но они делегировать прослушивание входящих сеансов и запросов службы toohello ретрансляции, размещенных в облаке. Ретранслятор Azure также защищает эти службы от несанкционированного доступа, применяя аутентификацию на основе [подписанного URL-адреса](../service-bus-messaging/service-bus-sas.md) (SAS).

## <a name="solution-scenario"></a>Сценарий решений
В этом учебнике вы создадите на веб-сайт ASP.NET, позволяющую toosee список продуктов на странице запасов продукции hello.

![][0]

Hello учебника предполагается, что иметь сведения о продукте в существующей локальной системе и использует tooreach Azure ретрансляции в этой системе. Это имитируется веб-службой, запущенной в простом консольном приложении и поддерживаемой набором продуктов в памяти. Необходимо будет toorun это консольное приложение на локальном компьютере и развернуть hello веб-роли в Azure. Таким образом, вы увидите как веб-роль hello в центре обработки данных Azure hello действительно вызвать на вашем компьютере, несмотря на то, что компьютер почти наверняка будет находиться по крайней мере один брандмауэр и слоя сетевой адрес преобразования Сетевых адресов.

## <a name="set-up-hello-development-environment"></a>Настройка среды разработки hello

Прежде чем начать, разработке приложений Azure, загрузите средства hello и настройка среды разработки:

1. Установить hello Azure SDK для .NET из пакета SDK для hello [страницу загрузки](https://azure.microsoft.com/downloads/).
2. В hello **.NET** столбец, выберите версию hello [Visual Studio](http://www.visualstudio.com) вы используете. Hello шаги в данном руководстве используйте Visual Studio 2015, но они также работают с Visual Studio 2017 г.
3. При запросе toorun или сохранить hello установщика нажмите **запуска**.
4. В hello **Web Platform Installer**, нажмите кнопку **установить** и продолжите установку hello.
5. После завершения установки hello, будет иметь все необходимые toostart приложение hello toodevelop. Hello SDK содержит средства, позволяющие легко разрабатывать приложения Azure в Visual Studio.

## <a name="create-a-namespace"></a>Создание пространства имен

с помощью toobegin Здравствуйте возможности ретрансляции в Azure, необходимо сначала создать пространство имен службы. Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении. Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.

## <a name="create-an-on-premises-server"></a>Создание локального сервера

Во-первых, нужно создать (макетную) локальную систему каталогов продукции. Он будет достаточно простой; Это можно увидеть, представляющее фактическое локальной системе каталога продукции с рабочей областью полный службы, что мы пытаетесь toointegrate.

Этот проект представляет собой консольное приложение Visual Studio и использует hello [пакет шины обслуживания Azure NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello библиотеки служебной шины и параметров конфигурации.

### <a name="create-hello-project"></a>Создание проекта hello

1. Запустите Microsoft Visual Studio, используя привилегии администратора. Таким образом, щелкните правой кнопкой мыши значок программы Visual Studio hello toodo и нажмите кнопку **Запуск от имени администратора**.
2. В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.
3. В разделе **Visual C#** области **Установленные шаблоны** щелкните **Консольное приложение (.NET Framework)**. В hello **имя** hello введите имя **ProductsServer**:

   ![][11]
4. Нажмите кнопку **ОК** toocreate hello **ProductsServer** проекта.
5. Если вы уже установили hello диспетчера пакетов NuGet для Visual Studio, пропустите следующий шаг toohello. В противном случае посетите сайт [NuGet][NuGet] и щелкните [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Установить NuGet). Выполните диспетчер пакетов NuGet hello tooinstall hello приглашения, а затем повторно запустите Visual Studio.
6. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsServer** проекта, а затем нажмите кнопку **управление пакетами NuGet**.
7. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Выберите hello **WindowsAzure.ServiceBus** пакета.
8. Нажмите кнопку **установить**и примите условия использования hello.

   ![][13]

   Обратите внимание, что требуемые hello, теперь существуют ссылки на сборки клиента.
8. Добавьте новый класс для контракта на свою продукцию. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsServer** проекта и нажмите кнопку **добавить**, а затем нажмите кнопку **класса**.
9. В hello **имя** hello введите имя **ProductsContract.cs**. Нажмите кнопку **Добавить**.
10. В **ProductsContract.cs**, замените следующий код, который определяет hello контракт для службы hello hello hello определения пространства имен.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. В файле Program.cs замените определение пространства имен hello hello, следующий код, который добавляет службы профиля hello и hello узла для него.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. В обозревателе решений дважды щелкните hello **App.config** файл tooopen его в редакторе Visual Studio hello. Внизу hello hello `<system.ServiceModel>` элемента (но по-прежнему в `<system.ServiceModel>`), добавьте следующий XML-кода hello. Быть убедиться, что tooreplace *yourServiceNamespace* с именем hello пространства имен, и *yourKey* с ключом SAS hello ранее получены из портала hello:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. По-прежнему в файл App.config, в hello `<appSettings>` элемента, замените значение строки подключения hello со строкой подключения hello ранее получены из портала hello.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Нажмите клавишу **Ctrl + Shift + B** или из hello **построения** меню, нажмите кнопку **построить решение** toobuild hello приложения и проверить правильность hello выполненной работы до сих.

## <a name="create-an-aspnet-application"></a>Создание приложения ASP.NET

В этом разделе будет выполнено построение простого приложения ASP.NET, которое будет отображать данные, полученные из службы продукции.

### <a name="create-hello-project"></a>Создание проекта hello

1. Убедитесь, что система Visual Studio запущена с правами администратора.
2. В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.
3. В разделе **Visual C#** области **Установленные шаблоны** щелкните **Веб-приложение ASP.NET (.NET Framework)**. Имя проекта hello **ProductsPortal**. Нажмите кнопку **ОК**.

   ![][15]

4. Из hello **шаблоны ASP.NET** списка в hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **MVC**.

   ![][16]

6. Нажмите кнопку hello **изменить аутентификацию** кнопки. В hello **изменить аутентификацию** диалогового окна убедитесь, что **без проверки подлинности** выбран и нажмите кнопку **ОК**. В этом руководстве развертывается приложение, для которого не требуется имя пользователя.

    ![][18]

7. Вернитесь на hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **ОК** приложение MVC toocreate hello.
8. Теперь необходимо настроить ресурсы Azure для нового веб-приложения. Следуйте указаниям hello hello [tooAzure части этой статьи публикации](../app-service-web/app-service-web-get-started-dotnet.md). Затем возвращают учебника toothis и продолжить toohello следующий шаг.
10. В обозревателе решений щелкните правой кнопкой мыши **Модели**, а затем выберите **Добавить** и **Класс**. В hello **имя** hello введите имя **Product.cs**. Нажмите кнопку **Добавить**.

    ![][17]

### <a name="modify-hello-web-application"></a>Изменить веб-приложение hello

1. В файле Product.cs hello в Visual Studio замените существующее определение пространства имен hello после кода hello.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. В обозревателе решений разверните hello **контроллеров** папки, дважды щелкните hello **HomeController.cs** файл tooopen его в Visual Studio.
3. В **HomeController.cs**, замените существующее определение пространства имен hello hello, следующий код.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. В обозревателе решений разверните hello одну папку, а затем дважды щелкните **_Layout.cshtml** tooopen его в редакторе Visual Studio hello.
5. Замените все вхождения **Мое приложение ASP.NET** слишком**продуктов LITWARE**.
6. Удалите hello **Главная**, **о**, и **контакт** ссылки. В следующем примере hello удалите код выделен hello.

    ![][41]

7. В обозревателе решений разверните папку Views\Home hello, а затем дважды щелкните **Index.cshtml** tooopen его в редакторе Visual Studio hello. Замените все содержимое файла hello hello hello, следующий код.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. tooverify hello точности своей работы таким образом, можно нажать клавишу **Ctrl + Shift + B** toobuild hello проекта.

### <a name="run-hello-app-locally"></a>Выполните приложение hello локально

Запустите tooverify приложения hello его работы.

1. Убедитесь, что **ProductsPortal** — hello активного проекта. Щелкните правой кнопкой мыши имя проекта hello в обозревателе решений и выберите **Назначить запускаемым проектом**.
2. В Visual Studio нажмите клавишу **F5**.
3. Приложение должно начать выполняться в браузере.

   ![][21]

## <a name="put-hello-pieces-together"></a>Объединить фрагменты hello

Hello следующим шагом является toohook копирование hello на локальном сервере продуктов с hello приложения ASP.NET.

1. Если он не открыт, в Visual Studio повторно открыть hello **ProductsPortal** проект, созданный в hello [создать приложение ASP.NET](#create-an-aspnet-application) раздела.
2. Аналогичный шаг toohello в разделе «Создать локальный сервер» hello, добавьте ссылки на проект toohello hello NuGet пакета. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **управление пакетами NuGet**.
3. Для поиска «Service Bus» и выберите hello **WindowsAzure.ServiceBus** элемента. Затем завершить установку hello и закрыть диалоговое окно.
4. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **добавить**, затем **существующий элемент**.
5. Перейдите toohello **ProductsContract.cs** файл из hello **ProductsServer** консольного проекта. Щелкните toohighlight ProductsContract.cs. Нажмите кнопку hello стрелку вниз рядом слишком**добавить**, нажмите кнопку **добавить как ссылку**.

   ![][24]

6. Теперь откройте hello **HomeController.cs** в редакторе Visual Studio hello и замените определение пространства имен hello hello, следующий код. Быть убедиться, что tooreplace *yourServiceNamespace* с именем hello пространства имен службы, и *yourKey* ваш ключ SAS. Это позволит hello клиента toocall hello локальной службы, возвращая результат hello hello вызова.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** решения (Убедитесь, что tooright щелчком hello решение, не hello проект). Щелкните **Добавить**, а затем — **Существующий проект**.
8. Перейдите toohello **ProductsServer** проекта, а затем дважды щелкните hello **ProductsServer.csproj** tooadd файл решения его.
9. **ProductsServer** на должна быть запущена в данные о заказах toodisplay hello **ProductsPortal**. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** решения и нажмите кнопку **свойства**. Hello **страницы свойств** диалоговое окно.
10. На hello слева, нажмите кнопку **запускаемый проект**. На правой стороне hello, нажмите кнопку **несколько запускаемых проектов**. Убедитесь, что **ProductsServer** и **ProductsPortal** отображается, в указанном порядке с **запустить** задать как действие hello для обоих.

      ![][25]

11. По-прежнему в hello **свойства** диалоговое окно, нажмите кнопку **зависимости проекта** на hello слева.
12. В hello **проекты** выберите **ProductsServer**. Снимите флажок **ProductsPortal**.
13. В hello **проекты** выберите **ProductsPortal**. Установите флажок **ProductsServer**.

    ![][26]

14. Нажмите кнопку **ОК** в hello **страницы свойств** диалоговое окно.

## <a name="run-hello-project-locally"></a>Запустите проект hello локально

приложения hello tootest локально, в Visual Studio нажмите клавишу **F5**. на локальном сервере Hello (**ProductsServer**) следует запустить первой, а затем hello **ProductsPortal** приложение должно запускаться в окне браузера. На этот раз вы увидите запасов продукта hello списки данных, полученных из hello продукта службы в локальной системе.

![][10]

Нажмите клавишу **обновление** на hello **ProductsPortal** страницы. Каждый раз, обновите страницу приветствия, вы увидите приложение hello server отображать сообщение при `GetProducts()` из **ProductsServer** вызывается.

Закройте оба приложения перед продолжением toohello следующий шаг.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Развертывание hello ProductsPortal проекта tooan веб-приложение Azure

Hello следующим шагом является toorepublish hello Azure Web app **ProductsPortal** переднего плана. Здравствуйте, следующие:

1. В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **публикации**. Нажмите кнопку **публикации** на hello **публикации** страницы.

  > [!NOTE]
  > Может появиться сообщение об ошибке в окне браузера hello при hello **ProductsPortal** веб-проекта запускается автоматически после развертывания hello. Это нормально и возникает из-за hello **ProductsServer** приложения еще не запущен.
>
>

2. Копировать URL-адрес hello объекта hello развернуть веб-приложения, как он потребуется hello URL-адрес в следующем шаге hello. Этот URL-адрес можно получить из окна hello активности службы приложения Azure в Visual Studio:

  ![][9]

3. Закройте hello окна браузера toostop hello запущено приложение.

### <a name="set-productsportal-as-web-app"></a>Настройка ProductsPortal в качестве веб-приложения

Прежде чем приложения hello в облаке hello, необходимо убедиться, что **ProductsPortal** , запускаемого из среды Visual Studio, что веб-приложение.

1. В Visual Studio щелкните правой кнопкой мыши hello **ProductsPortal** проект и выберите пункт **свойства**.
2. В левом столбце hello щелкните **Web**.
3. В hello **действие при запуске** щелкните hello **начальный URL-адрес** , а в hello текстовом поле введите URL-адрес hello ранее развернутого веб-приложения; например, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. Из hello **файл** меню в Visual Studio щелкните **сохранить все**.
5. В меню сборка hello в Visual Studio, нажмите кнопку **Перестроить решение**.

## <a name="run-hello-application"></a>Запустите приложение hello

1. Нажмите клавишу F5 toobuild и запустите приложение hello. на локальном сервере Hello (hello **ProductsServer** консольное приложение) следует запустить первой, а затем hello **ProductsPortal** приложение должно запускаться в окне браузера, как показано в следующий экран приветствия снимок. Снова Обратите внимание, запасов продукта hello перечислены данные, полученные из hello продукта службы в локальной системе и отображает их в веб-приложения hello. Проверьте что toomake URL-адрес hello, **ProductsPortal** работает в облаке hello, как Azure веб-приложение.

   ![][1]

   > [!IMPORTANT]
   > Hello **ProductsServer** консольного приложения должен быть запущен и может toohello данных hello tooserve **ProductsPortal** приложения. Если hello браузер отображает ошибку, подождите несколько секунд, дополнительные для **ProductsServer** tooload и отображения hello следующие сообщения. Нажмите клавишу **обновление** в браузере hello.
   >
   >

   ![][37]
2. Вернувшись в браузере hello, нажмите **обновление** на hello **ProductsPortal** страницы. Каждый раз, обновите страницу приветствия, вы увидите приложение hello server отображать сообщение при `GetProducts()` из **ProductsServer** вызывается.

    ![][38]

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о ретрансляции Azure см. следующие ресурсы hello.  

* [Что такое ретранслятор Azure?](relay-what-is-it.md)  
* [Как toouse ретрансляции](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
