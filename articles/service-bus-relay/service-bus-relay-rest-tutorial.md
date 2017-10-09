---
title: "Учебник по REST шины aaaService, с помощью ретрансляции Azure | Документы Microsoft"
description: "Создание простого ведущего приложения ретранслятора служебной шины Azure, которое предоставляет интерфейс на основе REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Руководство по REST для ретранслятора WCF Azure

В данном учебнике как toobuild простой ретранслятор Azure размещения приложения, предоставляющего интерфейс на основе REST. REST позволяет веб-клиента, такие как веб-браузер, hello tooaccess интерфейсов API служебной шины по протоколу HTTP-запросов.

Учебник Hello использует tooconstruct программирования модели hello REST Windows Communication Foundation (WCF) к службе REST Service Bus. Дополнительные сведения см. в разделе [модель программирования WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) и [проектирование и реализация служб](/dotnet/framework/wcf/designing-and-implementing-services) в документации по WCF hello.

## <a name="step-1-create-a-namespace"></a>Шаг 1. Создание пространства имен

с помощью toobegin Здравствуйте возможности ретрансляции в Azure, необходимо сначала создать пространство имен службы. Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении. Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>Шаг 2: Определение toouse контракта службы WCF на основе REST, с Azure ретрансляции

При создании WCF REST-службы, необходимо определить контракт hello. Контракт Hello указывает Здравствуйте, какие операции поддерживает узел. Операцию службы можно рассматривать как метод веб-службы. Контракты создаются путем определения интерфейса C++, C# или Visual Basic. Каждый метод в интерфейсе hello соответствует tooa определенной операции службы. Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) атрибут должен быть применен tooeach интерфейс и hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) атрибут должен быть применен tooeach операции. Если метод в интерфейсе, имеющем hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) имеет hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), что метод не предоставляется. Hello код для выполнения этих задач отображается в примере hello, после процедуры hello.

Hello основное различие между контракта WCF и контракт REST-является добавление hello toohello свойство [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Это свойство позволяет toomap метод в методе интерфейса tooa на hello другой стороне интерфейса hello. В этом случае мы используем [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP метод GET. Это позволяет Service Bus tooaccurately извлекать и интерпретировать команды, отправляемые toohello интерфейса.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate контракта с помощью интерфейса

1. Откройте Visual Studio с правами администратора: щелкните правой кнопкой мыши программу hello в hello **запустить** меню, а затем нажмите **Запуск от имени администратора**.
2. Создайте новый проект консольного приложения. Нажмите кнопку hello **файл** и выбрать пункт **New**, а затем выберите **проекта**. В hello **новый проект** диалоговое окно, нажмите кнопку **Visual C#**выберите hello **консольное приложение** шаблона и назовите его **ImageListener**. Использовать значение по умолчанию hello **расположение**. Нажмите кнопку **ОК** toocreate hello проекта.
3. Для проекта C# в Visual Studio создается файл с именем `Program.cs`. Этот класс содержит пустой `Main()` метод, необходимый для консольного приложения проекта toobuild правильно.
4. Добавьте ссылки на tooService шины и **System.ServiceModel.dll** toohello проекта путем установки пакета шины обслуживания NuGet hello. Этот пакет автоматически добавляет ссылки на библиотеки служебной шины toohello, а также hello WCF **System.ServiceModel**. В обозревателе решений щелкните правой кнопкой мыши hello **ImageListener** проекта, а затем нажмите кнопку **управление пакетами NuGet**. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Нажмите кнопку **установить**и примите условия использования hello.
5. Необходимо явно добавить ссылки слишком**System.ServiceModel.Web.dll** toohello проекта:
   
    а. В обозревателе решений щелкните правой кнопкой мыши hello **ссылки** папки в папку проекта hello, а затем нажмите кнопку **добавить ссылку**.
   
    b. В hello **добавить ссылку** диалоговое окно, нажмите кнопку hello **Framework** вкладка на левой стороне hello и hello **поиска** введите **System.ServiceModel.Web** . Выберите hello **System.ServiceModel.Web** флажок, а затем нажмите кнопку **ОК**.
6. Добавьте следующее hello `using` инструкций hello верхней части файла Program.cs hello.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello пространство имен, которое обеспечивает программный доступ toobasic возможности WCF. Ретрансляции WCF использует множество объектов hello и атрибутов контрактов службы WCF toodefine. Это пространство имен будет использоваться в большинстве приложений ретранслятора. Аналогичным образом [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) помогает определить канал hello, являющийся hello объекта, посредством которого осуществляется взаимодействие с веб-браузером клиента Azure ретрансляции и hello. Наконец [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) содержит hello типы, позволяющие toocreate веб-приложения.
7. Переименование hello `ImageListener` пространство имен слишком**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Непосредственно после фигурной деклараций пространств имен hello hello, определите новый интерфейс с именем **IImageContract** и применить hello **ServiceContractAttribute** интерфейс toohello атрибута с значение `http://samples.microsoft.com/ServiceModel/Relay/`. Значение пространства имен Hello отличается от hello пространства имен, используемого во всей области действия своего кода hello. Значение пространства имен Hello используется в качестве уникального идентификатора для данного контракта и должно содержать сведения о версии. Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498). Явное указание пространства имен hello запрещает значение пространства имен по умолчанию hello toohello имя контракта.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. В рамках hello `IImageContract` интерфейсом, объявите метод для отдельной операции hello hello `IImageContract` предоставляет контракт в hello интерфейс и применение hello `OperationContractAttribute` атрибута toohello способ tooexpose как часть службы открытого hello шины контракт.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. В hello **OperationContract** , добавьте hello **WebGet** значение.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Таким образом, включает hello tooroute службы ретрансляции HTTP-запросы GET слишком`GetImage`и значений, возвращаемых из hello tootranslate `GetImage` в ответ HTTP GETRESPONSE. Далее в учебнике hello используется tooaccess веб браузера этот метод и toodisplay hello изображения в браузере hello.
11. Непосредственно после hello `IImageContract` определение, объявите канал, который наследует от обоих hello `IImageContract` и `IClientChannel` интерфейсов.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Канал представляет hello объекта WCF, через который hello службы и клиента передачи tooeach сведения о других. Позже можно создать канал hello в основное приложение. Ретранслятор Azure затем использует этот канал toopass hello HTTP-запросы GET из браузера tooyour hello **GetImage** реализации. Hello ретрансляции также использует hello канала tootake hello **GetImage** возвращаемое значение и преобразовать его в ответ HTTP GETRESPONSE для браузера клиента hello.
12. Из hello **построения** меню, нажмите кнопку **построить решение** tooconfirm hello правильность выполненной работы к текущему моменту.

### <a name="example"></a>Пример
Hello после кода показан базовый интерфейс, определяющий контракт ретрансляции WCF.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Шаг 3: Реализация toouse контракта службы WCF на основе REST Service Bus
Создание службы ретрансляции WCF в стиле REST необходимо сначала создать контракт hello, который определен с помощью интерфейса. Hello следующим шагом является интерфейс tooimplement hello. Это предполагает создание класса с именем **ImageService** , реализующий hello определяемых пользователем **IImageContract** интерфейса. После реализации контракта hello, необходимо настроить интерфейс hello, с помощью файла App.config. Hello файл конфигурации содержит сведения, необходимые для приложения hello, например имя службы hello hello, hello hello контракта и тип протокола, используемые toocommunicate со службой ретрансляции hello hello. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.

Как и hello предыдущие действия, существует очень небольшая разница в реализации контракт REST- и контракта WCF ретрансляции.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>Контракт tooimplement стиле REST Service Bus
1. Создайте новый класс с именем **ImageService** непосредственно после определения hello hello **IImageContract** интерфейса. Hello **ImageService** класс реализует hello **IImageContract** интерфейса.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Определение hello схожие реализации интерфейса tooother, можно реализовать в другой файл. Однако в этом учебнике реализация hello появляется в тот же файл как определение интерфейса hello hello и `Main()` метод.
2. Применить hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) атрибута toohello **IImageService** tooindicate класс, который hello класс — это реализация контракта WCF.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Как упоминалось ранее, это пространство имен не является обычным. Вместо этого он является частью WCF архитектуру, которая идентифицирует контракт hello hello. Дополнительные сведения см. в разделе hello [имена контрактов данных](https://msdn.microsoft.com/library/ms731045.aspx) раздела hello документации WCF.
3. Добавьте проект tooyour .jpg изображения.  
   
    Это рисунок, службой hello в hello получение браузера. Щелкните проект правой кнопкой мыши и выберите **Добавить**. Затем выберите **Существующий элемент**. Используйте hello **Добавление существующего элемента** tooan toobrowse поле диалогового окна, возможно .jpg и нажмите кнопку **добавить**.
   
    При добавлении файла hello, убедитесь, что **все файлы** в toohello Далее hello раскрывающемся списке выбран **имя файла:** поля. Hello конца данного учебника предполагается, что hello hello изображение называется «image.jpg». Если имеется другой файл, будет toorename hello образ или изменить toocompensate вашего кода.
4. hello, что запущена служба могли находить в файл изображения hello, toomake **обозревателе решений** щелкните правой кнопкой мыши файл изображения hello, а затем нажмите кнопку **свойства**. В hello **свойства** задайте **скопируйте каталог tooOutput** слишком**копировать, если новее**.
5. Добавить toohello ссылки **System.Drawing.dll** toohello сборки проекта, а также добавить hello следующие связанные `using` инструкции.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. В hello **ImageService** добавьте hello за конструктором, загружаются hello точечный рисунок и подготавливает toosend его toohello клиентского браузера.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Непосредственно после кода предыдущего hello добавьте следующее hello **GetImage** метод в hello **ImageService** класса tooreturn HTTP сообщения, содержащего изображение hello.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Эта реализация использует **MemoryStream** tooretrieve hello изображения и подготовить его для потоковой передачи toohello браузера. Запускает hello нуля позицию потока, объявляет содержимое потока hello в формате jpeg и отправляет сведения hello.
8. Из hello **построения** меню, нажмите кнопку **построить решение**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>Конфигурация hello toodefine запустить hello веб-службы для служебной шины
1. В **обозревателе решений**, дважды щелкните **App.config** tooopen его в редакторе Visual Studio hello.
   
    Hello **App.config** файл, содержащий имя службы hello, конечной точки (то есть hello расположение ретрансляции Azure предоставляет клиентам и узлам toocommunicate друг с другом) и привязки (hello тип протокола, который будет использоваться toocommunicate). Hello основное различие состоит в этой конечной точкой службы настроены hello ссылается tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) привязки.
2. Hello `<system.serviceModel>` XML-элемент — это элемент WCF, который определяет одну или несколько служб. В данном случае имя службы используется toodefine hello и конечной точки. Внизу hello hello `<system.serviceModel>` элемент (но по-прежнему в `<system.serviceModel>`), добавить `<bindings>` элемент, имеющий hello после содержимого. Этот параметр определяет hello привязки, используемые в приложении hello. Можно определить несколько привязок, но в этом учебнике определяется только одна.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    Предыдущий код Hello определяет ретрансляции WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) привязки с **relayClientAuthenticationType** значение слишком**нет**. Этот параметр указывает, что для конечной точки, использующей эту привязку, не требуются учетные данные клиента.
3. После hello `<bindings>` элемента, добавьте `<services>` элемента. Аналогичными привязками toohello можно определить несколько служб в одном файле конфигурации. Но в этом учебнике определяется только одна.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Этот шаг позволяет настроить службу, которая использует по умолчанию hello ранее определенные **webHttpRelayBinding**. Кроме того, используются по умолчанию hello **sbTokenProvider**, которая определена в следующем шаге hello.
4. После hello `<services>` элемент, создайте `<behaviors>` элемент с hello вслед содержимым, заменив «SAS_KEY» hello *подписи общего доступа* ключа (SAS), ранее получены из hello [портал Azure ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. По-прежнему в файл App.config, в hello `<appSettings>` элемент замены hello все подключение строковое значение со строкой подключения hello ранее получены из портала hello. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Из hello **построения** меню, нажмите кнопку **построить решение** toobuild hello всего решения.

### <a name="example"></a>Пример
Hello код отображает hello контракта и реализации службы для службы на основе REST, которая выполняется на Service Bus с помощью hello **WebHttpRelayBinding** привязки.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Hello пример hello файла App.config, связанного со службой hello.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>Шаг 4: Размещения toouse службы WCF на основе REST hello Azure ретрансляции
В этом разделе описывается, как toorun веб-узел службы с помощью консольного приложения с WCF ретрансляции. Полный листинг кода hello, написанного на этом шаге приведен в примере hello, после процедуры hello.

### <a name="toocreate-a-base-address-for-hello-service"></a>toocreate базовый адрес для службы hello
1. В hello `Main()` объявление функции, создать пространство имен переменной toostore hello проекта. Убедитесь, что tooreplace `yourNamespace` с именем hello пространства имен hello ретрансляции, созданную ранее.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Service Bus использует имя hello в пространство имен toocreate уникальный URI.
2. Создание `Uri` экземпляр hello базового адреса службы hello, основанный на пространство имен hello.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate и настроить узел веб-службы hello
* Создайте hello узел веб-службы, с помощью созданного ранее в этом разделе hello URI-адрес.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    узел службы Hello: hello объекта WCF, который создает экземпляры ведущего приложения hello. В этом примере передается hello тип узла требуется toocreate ( **ImageService**), а также hello адрес, по которому требуется tooexpose hello ведущего приложения.

### <a name="toorun-hello-web-service-host"></a>узел toorun hello веб-служб
1. Откройте службу hello.
   
    ```csharp
    host.Open();
    ```
    Теперь Hello служба работает.
2. Сообщение, указывающее, что запущена служба hello и как toostop hello службы.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. После завершения закройте узел службы hello.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Пример
Следующий пример Hello включает hello контракт и реализацию службы из предыдущих шагов в hello учебник и узлы служб hello в консольном приложении. Скомпилируйте следующий код в исполняемый файл с именем ImageListener.exe hello.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Компиляция кода hello
После построения решения hello, hello следующие приложения hello toorun:

1. Нажмите клавишу **F5**, или найдите расположение исполняемого файла toohello (ImageListener\bin\Debug\ImageListener.exe) toorun hello службы. Оставьте hello приложение выполняется, так как он является обязательным, следующим шагом tooperform hello.
2. Скопируйте и вставьте адрес hello из командной строки hello в изображение hello toosee браузера.
3. Когда вы закончите, нажмите клавишу **ввод** в приложение hello tooclose окно командной строки hello.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы создали приложение, использующее службы ретрансляции Service Bus hello, см. следующие статьи toolearn больше о Azure ретрансляции hello.

* [Обзор архитектуры служебной шины Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Как службу в .NET Framework посредника toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
