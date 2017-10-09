---
title: "Учебник ретрансляции WCF Service Bus aaaAzure | Документы Microsoft"
description: "Создание службы и клиентского приложения служебной шины с помощью ретранслятора WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Руководство по ретранслятору WCF Azure

В данном учебнике как toobuild простой WCF ретрансляции клиентского приложения и службы с помощью Azure ретрансляции. Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Прохождение этого учебника дает представление о hello шаги, необходимые toocreate приложении клиента и службы ретрансляции WCF. Как и в WCF, под службой понимается конструкция, которая предоставляет одну или несколько конечных точек, каждая из которых предоставляет одну или несколько операций службы. Hello конечную точку службы определяет адрес, где можно найти службу hello, привязка, которая содержит сведения hello, клиент должен связаться с hello службы и контракт, определяющий hello функциональные возможности, предоставляемые клиентами tooits hello службы. Hello основное различие между WCF и ретрансляции WCF — в облаке hello, а не на локальном компьютере, предоставленный этой конечной точке hello.

После работы через последовательность hello разделов в этом учебнике будет иметь запущенной службы и клиента, который можно вызвать операции hello hello службы. Hello первой статье описывается, как tooset учетную запись. Hello Далее описывается, как toodefine службы, использует контракт, как tooimplement hello службы и как tooconfigure hello службы в коде. В них также рассматриваются как toohost и запустите службу hello. Hello созданная служба является резидентной и hello клиент и служба работают на hello того же компьютера. Можно настроить службу hello с помощью кода или файла конфигурации.

Hello заключительные три действия описывают, как toocreate клиентского приложения, настройте клиентское приложение hello и создать и использовать клиент, который можно получить доступ к функциональности hello hello узла.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника вам потребуется hello следующие:

* [Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com). В этом учебнике используется Visual Studio 2017.
* Активная учетная запись Azure. Если ее нет, можно создать бесплатную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Создание пространства имен службы

Hello первым шагом является toocreate пространства имен и tooobtain [подписи общего доступа (SAS)](../service-bus-messaging/service-bus-sas.md) ключа. Пространство имен предоставляет границу для каждого приложения, предоставляемые через службу ретрансляции hello. Ключ SAS автоматически создается системой hello при создании пространства имен службы. Hello сочетание пространства имен службы и ключ SAS содержит учетные данные hello Azure tooauthenticate доступа tooan приложения. Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.

## <a name="define-a-wcf-service-contract"></a>Определение контракта службы WCF

контракт службы Hello указывает, какие службы поддерживает hello операций (hello термины веб-служб для методов или функций). Контракты создаются путем определения интерфейса C++, C# или Visual Basic. Каждый метод в интерфейсе hello соответствует tooa определенной операции службы. Каждый интерфейс должен иметь hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit применен атрибут, и каждая операция должна иметь hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit применен атрибут. Если метод в интерфейсе, имеющем hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) атрибут не имеет hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) атрибута, метод не предоставляется. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello. Более полное обсуждение контрактов и служб в разделе [проектирование и реализация служб](https://msdn.microsoft.com/library/ms729746.aspx) в документации по WCF hello.

### <a name="create-a-relay-contract-with-an-interface"></a>Создание контракта ретранслятора с помощью интерфейса

1. Откройте Visual Studio с правами администратора, щелкнув правой кнопкой мыши программу hello в hello **запустить** , выберите в меню **Запуск от имени администратора**.
2. Создайте новый проект консольного приложения. Нажмите кнопку hello **файл** и выбрать пункт **New**, нажмите кнопку **проекта**. В hello **новый проект** диалоговое окно, нажмите кнопку **Visual C#** (если **Visual C#** не отображается, найдите его в разделе **другие языки**). Нажмите кнопку hello **консольного приложения (.NET Framework)** шаблона и назовите его **EchoService**. Нажмите кнопку **ОК** toocreate hello проекта.

    ![][2]

3. Установите пакет шины обслуживания NuGet hello. Этот пакет автоматически добавляет ссылки на библиотеки служебной шины toohello, а также hello WCF **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello пространство имен, которое позволяет tooprogrammatically доступа hello основные компоненты служб WCF. Шина обслуживания использует множество объектов hello и атрибутов контрактов службы WCF toodefine.

    В обозревателе решений щелкните правой кнопкой мыши проект hello и нажмите кнопку **управление пакетами NuGet...** . Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Убедитесь, что имя проекта hello в hello **версии** поле. Нажмите кнопку **установить**и примите условия использования hello.

    ![][3]
4. В обозревателе решений дважды щелкните tooopen файл Program.cs hello, откройте его в редакторе hello, если его еще нет.
5. Добавьте hello следующие операторы using в начало hello hello файла:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Изменить имя пространства имен hello с его имя по умолчанию **EchoService** слишком**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > В этом учебнике используется пространство имен hello C# **Microsoft.ServiceBus.Samples**, это пространство имен hello hello на основе контракта управляемого типа, который используется в файле конфигурации hello в hello [клиента WCF hello Настройка](#configure-the-wcf-client) шаг. Можно задать любое пространство имен, необходимые при выполнении сборки этого примера; Однако hello Учебник не будет работать, если вы измените hello пространства имен контракта hello и службы соответственно, в файле конфигурации приложения hello. приветствия имен, указанное в hello App.config, файл должен быть таким же hello hello пространства имен, указанные в файлах C#.
   >
   >
7. Непосредственно после hello `Microsoft.ServiceBus.Samples` объявление пространства имен, но в пространстве имен hello, определите новый интерфейс с именем `IEchoContract` и применить hello `ServiceContractAttribute` интерфейс toohello атрибут со значением пространства имен `http://samples.microsoft.com/ServiceModel/Relay/`. Значение пространства имен Hello отличается от hello пространства имен, используемого во всей области действия своего кода hello. Вместо этого значение hello пространства имен используется как уникальный идентификатор для данного контракта. Явное указание пространства имен hello запрещает значение пространства имен по умолчанию hello toohello имя контракта. Вставьте следующий код после объявления пространства имен hello hello:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Как правило пространство имен контракта службы hello содержит схему именования, которая содержит сведения о версии. Включая сведения о версии в пространство имен контракта службы hello включает службы tooisolate значительные изменения, определяя новый контракт службы с новым пространством имен и предоставляя его в новую конечную точку. Таким образом клиенты можно продолжить без необходимости обновить toobe toouse hello старый контракт службы. Сведения о версии могут включать дату и номер сборки. Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498). Для целей этого учебника hello схему пространства имен контракта службы hello именования hello не содержит сведений о версии.
   >
   >
8. В рамках hello `IEchoContract` интерфейсом, объявите метод для отдельной операции hello hello `IEchoContract` предоставляет контракт в hello интерфейс и применение hello `OperationContractAttribute` метод toohello атрибут, который вы хотите tooexpose как часть hello открытые ретрансляции WCF контракт, как показано ниже:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Непосредственно после hello `IEchoContract` определение интерфейса, объявите канал, который наследует от обоих `IEchoContract` и также toohello `IClientChannel` интерфейс, как показано ниже:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Канал представляет hello объекта WCF, через который hello служба и клиент обмениваются tooeach сведения о других. Более поздней версии вы напишете код для hello сведения tooecho канал между двумя приложениями hello.
10. Из hello **построения** меню, нажмите кнопку **построить решение** или нажмите клавишу **Ctrl + Shift + B** tooconfirm hello правильность выполненной работы до сих.

### <a name="example"></a>Пример

Hello после кода показан базовый интерфейс, определяющий контракт ретрансляции WCF.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Теперь, когда hello интерфейс создан, можно реализовать интерфейс hello.

## <a name="implement-hello-wcf-contract"></a>Реализация контракта WCF hello

Создание ретрансляции Azure требуется сначала создать контракт hello, который определен с помощью интерфейса. Дополнительные сведения о создании интерфейса hello см. предыдущий шаг hello. Hello следующим шагом является интерфейс tooimplement hello. Это предполагает создание класса с именем `EchoService` , реализующий hello определяемых пользователем `IEchoContract` интерфейса. После реализации интерфейса hello, необходимо настроить интерфейс hello, с помощью файла конфигурации App.config. Hello файл конфигурации содержит сведения, необходимые для приложения hello, например имя службы hello hello, hello hello контракта и тип протокола, используемые toocommunicate со службой ретрансляции hello hello. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello. Более общие сведения о как tooimplement службы контракта, в разделе [реализация контрактов службы](https://msdn.microsoft.com/library/ms733764.aspx) в документации по WCF hello.

1. Создайте новый класс с именем `EchoService` непосредственно после определения hello hello `IEchoContract` интерфейса. Hello `EchoService` класс реализует hello `IEchoContract` интерфейса.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Определение hello схожие реализации интерфейса tooother, можно реализовать в другой файл. Однако в этом учебнике реализация hello расположена в тот же файл определения интерфейса hello и hello hello `Main` метод.
2. Применить hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) атрибута toohello `IEchoContract` интерфейса. атрибут Hello указывает имя службы hello и пространства имен. После этого hello `EchoService` класс имеет следующий вид:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Реализуйте hello `Echo` метода, определенного в hello `IEchoContract` интерфейса в hello `EchoService` класса.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Нажмите кнопку **построения**, нажмите кнопку **построить решение** tooconfirm hello точности своей работы.

### <a name="define-hello-configuration-for-hello-service-host"></a>Определение конфигурации hello для узла службы hello

1. файл конфигурации Hello — очень похожих файлов конфигурации WCF tooa. Он включает имя службы hello, конечной точки (расположение hello, ретрансляции Azure предоставляет клиентам и узлам toocommunicate друг с другом) и hello привязку (тип протокола, используемые toocommunicate hello). Hello основное отличие состоит в том, что эта конечная точка службы, настроенные ссылается tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) привязки, который не является частью .NET Framework hello. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) одна из привязок hello определены службой hello.
2. В **обозревателе решений**, tooopen файл App.config hello дважды щелкните его в редакторе Visual Studio hello.
3. В hello `<appSettings>` элемента, замените заполнители hello hello имя пространства имен службы и hello ключ SAS, скопированный на предыдущем шаге.
4. В рамках hello `<system.serviceModel>` добавление тегов, `<services>` элемент. В отдельном файле конфигурации можно определить несколько приложений ретранслятора. Однако в данном учебнике определяется только одно приложение.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. В рамках hello `<services>` элемента, добавьте `<service>` элемент toodefine hello имя службы hello.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. В рамках hello `<service>` элемента, определение расположения hello hello контракта конечной точки, а также hello тип привязки для конечной точки hello.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    Hello конечная точка определяет, где hello клиент будет искать ведущее приложение hello. Позже hello учебнике этот шаг toocreate URI, который полностью предоставляет узел hello посредством Azure ретрансляции. Привязка Hello указывает, что мы используем TCP как hello протокола toocommunicate со службой ретрансляции hello.
7. Из hello **построения** меню, нажмите кнопку **построить решение** tooconfirm hello точности своей работы.

### <a name="example"></a>Пример

Hello следующем примере кода показана реализация hello hello контракт службы.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Hello следующий код показывает hello стандартный формат файла App.config hello, связанный с узлом службы hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Размещение и запуск tooregister простой службы со службой ретрансляции hello

В этом разделе описывается, как toorun Azure ретрансляции службы.

### <a name="create-hello-relay-credentials"></a>Создать учетные данные для ретрансляции hello

1. В `Main()`, создайте две переменные в пространстве имен hello какие toostore и ключ SAS, считываемых из окна консоли hello hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    ключ SAS Hello будет tooaccess используется более поздней версии проекта. пространство имен Hello передается как параметр слишком`CreateServiceUri` toocreate URI службы.
2. С помощью [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) объекта, объявите, что вы будете использовать ключ SAS как hello тип учетных данных. Добавьте следующий код непосредственно после hello код, добавленный в последнем шаге hello hello.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Создайте базовый адрес службы hello

После кода hello, добавленный в последнем шаге hello, создайте `Uri` экземпляр hello базового адреса службы hello. Этот URI указывает схему Service Bus hello, пространство имен hello и hello путь интерфейса службы hello.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

«sb»-это сокращение для схемы Service Bus hello и указывает, что мы используем hello протокол TCP. Это также ранее определено в файле конфигурации hello, когда [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) был указан как hello привязки.

В этом учебнике hello URI является `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Создание и настройка узла службы hello

1. Установить режим подключения hello слишком`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    режим подключения Hello описывает hello протокола hello использует toocommunicate со службой ретрансляции hello; HTTP или TCP. Использование параметра по умолчанию hello `AutoDetect`, hello служба пытается tooconnect tooAzure ретрансляции через TCP, если он доступен и HTTP, если TCP недоступен. Обратите внимание, что это отличается от службы hello протокола hello указывает для связи с клиентами. Этот протокол определяется hello привязку, используемую. Например, служба может использовать hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) привязки, который указывает, что ее конечная точка связывается с клиентами по протоколу HTTP. Что же службе может указать **ConnectivityMode.AutoDetect** , чтобы служба hello взаимодействует с Azure ретрансляции по протоколу TCP.
2. Создайте узел службы hello, используя приветствия URI созданного ранее в этом разделе.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    узел службы Hello: hello объекта WCF, создающий экземпляр службы hello. Здесь можно передать его тип hello службы требуется toocreate ( `EchoService` типа) и также toohello адрес, по которому требуется служба tooexpose hello.
3. Вверху hello hello файла Program.cs добавьте ссылки на слишком[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) и [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. В `Main()`, настройте hello конечной точки tooenable общего доступа.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Это действие позволяет сообщить hello служба ретрансляции, что приложения могут быть найдены публично изучив hello веб-канал ATOM для проекта. Если задать **DiscoveryType** слишком**закрытый**, клиент по-прежнему будет службы может tooaccess hello. Тем не менее служба hello не будет отображаться, когда он выполняет поиск пространства имен ретрансляции hello. Вместо этого клиент hello будет иметь путь конечной точки tooknow hello заранее.
5. Применить toohello конечные точки, определенные в файле App.config hello, учетные данные службы hello:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Как уже говорилось в предыдущем шаге hello, удалось объявлен несколько служб и конечных точек в файле конфигурации hello. Если у вас есть, передается этот код в файле конфигурации hello и поиска для каждой конечной точки toowhich его следует применять свои учетные данные. Однако в этом учебнике hello файл конфигурации имеет только одну конечную точку.

### <a name="open-hello-service-host"></a>Привет открыть узел службы

1. Откройте службу hello.

    ```csharp
    host.Open();
    ```
2. Уведомить пользователя hello, hello служба запущена и объясняется, как tooshut работу службы hello.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. После завершения закройте узел службы hello.

    ```csharp
    host.Close();
    ```
4. Нажмите клавишу **Ctrl + Shift + B** toobuild hello проекта.

### <a name="example"></a>Пример

Готовый код службы должен выглядеть так, как показано ниже. Код Hello включает hello контракт и реализацию службы из предыдущих шагов в учебнике hello и узлы hello службы в консольном приложении.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Создание клиента WCF для контракта службы hello

Следующий шаг Hello toocreate клиентское приложение и определить hello контракт службы, которая будет создана на последующих этапах. Обратите внимание, что многие из этих шагов похожие шаги hello использовать toocreate службы: определение контракта, изменение App.config текстовый файл, с помощью службы ретранслятора toohello tooconnect учетные данные и т. д. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.

1. Создайте новый проект в текущем решении Visual Studio hello для hello клиента, выполнив hello ниже:

   1. В обозревателе решений в решение, содержащее службу hello hello, щелкните правой кнопкой мыши hello текущего решения (не проект hello) и нажмите кнопку **добавить**. Выберите **Создать проект**.
   2. В hello **Добавление нового проекта** диалоговое окно, нажмите кнопку **Visual C#** (если **Visual C#** не отображается, найдите его в разделе **другие языки**) выберите hello **Консольного приложения (.NET Framework)** шаблона и назовите его **EchoClient**.
   3. Нажмите кнопку **ОК**.
      <br />
2. В обозревателе решений дважды щелкните файл Program.cs hello в hello **EchoClient** проекта tooopen, откройте его в редакторе hello, если его еще нет.
3. Изменить имя пространства имен hello с его имя по умолчанию `EchoClient` слишком`Microsoft.ServiceBus.Samples`.
4. Установка hello [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus): в обозревателе решений щелкните правой кнопкой мыши hello **EchoClient** проекта, а затем нажмите кнопку **управление пакетами NuGet**. Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`. Нажмите кнопку **установить**и примите условия использования hello.

    ![][3]
5. Добавить `using` инструкции для hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) пространства имен в файл Program.cs hello.

    ```csharp
    using System.ServiceModel;
    ```
6. Добавьте hello определения toohello пространства имен контракта службы, как показано в следующий пример hello. Обратите внимание, что это определение идентичные toohello определение, используемое в hello **службы** проекта. Этот код следует добавить вверху hello hello `Microsoft.ServiceBus.Samples` пространства имен.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Нажмите клавишу **Ctrl + Shift + B** toobuild hello клиента.

### <a name="example"></a>Пример

Hello следующий код показывает текущее состояние файла Program.cs hello hello в hello **EchoClient** проекта.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Настройка клиента WCF hello

На этом шаге создается файл App.config для простом клиентском приложении, которое обращается к службе hello, созданной ранее в этом учебнике. Этот файл App.config определяет hello контракта, привязки и имя конечной точки hello. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.

1. В обозревателе решений в hello **EchoClient** проекта, дважды щелкните **App.config** tooopen hello файл в редакторе Visual Studio hello.
2. В hello `<appSettings>` элемента, замените заполнители hello hello имя пространства имен службы и hello ключ SAS, скопированный на предыдущем шаге.
3. В элементе управления system.serviceModel hello, добавьте `<client>` элемента.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    На этом шаге вы объявляете, что определяете клиентское приложение WCF.
4. В рамках hello `client` элемент, определите hello имя контракта и тип привязки для конечной точки hello.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Этот шаг определяет имя hello hello конечной точки, hello контракт, определенный в службу hello и hello факт, что hello клиентское приложение использует TCP toocommunicate с Azure ретрансляции. Hello имя конечной точки используется в hello следующий шаг toolink конфигурацию конечной точки URI службы hello.
5. В меню **Файл** выберите **Сохранить все**.

## <a name="example"></a>Пример

Hello код отображает hello файл App.config для клиента Echo hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Реализуйте клиент WCF hello
На этом шаге вы реализовать простом клиентском приложении, которое обращается к службе hello, созданный ранее в этом учебнике. Аналогичную службу toohello hello клиент выполняет множество таких hello же операции tooaccess ретрансляции Azure:

1. Задает режим подключения hello.
2. Создает URI расположения узла службы hello hello.
3. Определяет учетные данные безопасности hello.
4. Применяет подключение toohello hello учетные данные.
5. Открывает соединение hello.
6. Выполняет задачи, связанные с приложение hello.
7. Закрывает соединение hello.

Одно из основных различий hello то, что hello клиентское приложение использует службу ретрансляции toohello tooconnect канала, в то время как hello служба использует вызов слишком**ServiceHost**. Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.

### <a name="implement-a-client-application"></a>Реализация клиентского приложения
1. Установить режим подключения hello слишком**Автообнаружение**. Добавьте следующий код внутри hello hello `Main()` метод hello **EchoClient** приложения.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Определите переменные toohold hello значения для пространства имен службы hello и ключ SAS, считываемых с консоли hello.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Создайте hello URI, определяющий расположение узла hello hello в проекте ретрансляции.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Создайте hello объекта учетных данных для конечной точки пространства имен службы.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Создайте фабрику каналов hello, загружает конфигурацию hello, описанных в файле App.config hello.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Фабрику каналов является объектом WCF, который создает канал, через который взаимодействия служб и клиентских приложений hello.
6. Примените учетные данные hello.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Создайте и откройте hello канала toohello службы.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Запись hello основной пользовательский интерфейс и функциональные возможности для hello echo.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Обратите внимание, что hello код использует экземпляр hello hello объекта канала как прокси для службы hello.
9. Закройте канал hello и закрыть hello фабрики.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Пример

Отображается как toocreate клиентского приложения, как toocall hello операции службы hello и как tooclose hello клиента после операции hello вызвать завершения завершенного код должен выглядеть следующим образом.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Запускать приложения hello

1. Нажмите клавишу **Ctrl + Shift + B** toobuild hello решения. При этом строится hello клиентский проект и проект службы hello, созданный на предыдущих этапах hello.
2. Перед запущенному hello клиентскому приложению необходимо убедитесь, что приложение hello-служба запущена. В обозревателе решений в Visual Studio, щелкните правой кнопкой мыши hello **EchoService** решение, нажмите кнопку **свойства**.
3. В диалоговое окно «Свойства» для hello решение, нажмите кнопку **запускаемый проект**, нажмите кнопку hello **несколько запускаемых проектов** кнопки. Убедитесь, что **EchoService** отображается первым в списке hello.
4. Набор hello **действия** поле для обоих hello **EchoService** и **EchoClient** проекты слишком**запустить**.

    ![][5]
5. Щелкните **Зависимости проектов**. В hello **проекты** выберите **EchoClient**. В hello **зависит от** убедитесь, что **EchoService** проверяется.

    ![][6]
6. Нажмите кнопку **ОК** toodismiss hello **свойства** диалогового окна.
7. Нажмите клавишу **F5** toorun обоих проектов.
8. В обоих окнах консоли откройте и указать имя пространства имен hello. Hello служба должна запускаться сначала, поэтому в hello **EchoService** окна консоли введите пространство имен hello и нажмите клавишу **ввод**.
9. Далее появится запрос на ввод ключа SAS. Введите ключ SAS hello и нажмите клавишу ВВОД.

    Ниже приведен пример выходных данных из окна консоли hello. Обратите внимание, что значения hello приведены здесь пример исключительно в целях.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    приложение службы Hello печатает toohello окна консоли hello адрес, который он прослушивает, как видно в следующий пример hello.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. В hello **EchoClient** окно консоли, введите hello же сведения, введенные ранее для приложения службы hello. Выполните hello предыдущего действия tooenter hello одинаковое пространство имен службы и SAS ключевые значения для клиентского приложения hello.
11. После ввода значений, клиент hello открывает канал toohello службы и предлагает вам tooenter текст, как показано в следующий пример выходных данных консоли hello.

    `Enter text tooecho (or [Enter] tooexit):`

    Введите некоторые приложения службы toohello toosend текст и нажмите клавишу ВВОД. Этот текст отправляется службе toohello через hello эхо-повтор операции службы, отображается в окне консоли службы hello как hello следующий пример выходных данных.

    `Echoing: My sample text`

    клиентское приложение Hello получает возвращаемое значение hello hello `Echo` операцию, которая является исходный текст hello и печатает его в окно консоли tooits. Hello ниже приведен пример выходных данных в окне консоли клиента hello.

    `Server echoed: My sample text`
12. Можно продолжить отправлять текстовые сообщения от службы toohello hello клиента таким образом. Когда закончите, нажмите клавишу ВВОД в hello клиента и службы консоли windows tooend обоих приложений.

## <a name="next-steps"></a>Дальнейшие действия

Этого учебника было показано, как toobuild клиентского приложения Azure ретрансляции и службы с помощью hello возможности ретрансляции WCF Service Bus. Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn Дополнительные сведения о ретрансляции Azure см. следующие разделы hello.

* [Обзор архитектуры служебной шины Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Как службу в .NET Framework посредника toouse hello WCF](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
