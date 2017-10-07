---
title: "aaaGet работы с Azure ретрансляции WCF ретрансляции в .NET | Документы Microsoft"
description: "Узнайте, как toouse Azure WCF ретрансляции ретранслирует tooconnect двух приложений, размещенных в разных местах."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Как toouse Azure ретрансляции WCF ретрансляций с .NET
В этой статье описывается, как toouse hello служба ретрансляции Azure. Hello примеры написаны на C# и использовать API Windows Communication Foundation (WCF) hello с расширениями, содержащихся в hello сборки служебной шины. Дополнительные сведения о Azure ретрансляции см. в разделе hello [Обзор Azure ретрансляции](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>Что такое ретранслятор WCF?

Hello Azure [ *ретрансляции WCF* ](relay-what-is-it.md) служба позволяет toobuild гибридных приложений, которые запускаются в центре обработки данных Azure и среде предприятия в локальной среде. служба ретрансляции Hello облегчает это, позволяя toosecurely предоставлять службы Windows Communication Foundation (WCF), которые находятся в корпоративной среде организации сети toohello общедоступное облако, без необходимости tooopen подключения брандмауэра или требования Инфраструктура корпоративной сети tooa влияние изменений.

![Обзор ретранслятора WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Ретранслятор Azure позволяет toohost служб WCF в существующей среде предприятия. Затем можно делегировать прослушивание входящих сеансов и запросов toothese WCF toohello ретрансляции службы, запущенные в Azure. Благодаря этому вы tooexpose эти службы tooapplication код, выполняющийся в Azure, или toomobile работников или экстрасети партнера сред. Ретрансляции позволяет toosecurely контролировать, кто может обращаться к службам на уровне детально. Она обеспечивает функциональные возможности приложений tooexpose мощные и безопасный способ и данных из существующих решений и использовать преимущества ее из облака hello.

Здесь рассматривается как toocreate toouse ретрансляции Azure предоставляется с помощью привязки канала TCP, который реализует безопасного обмена данными между двумя сторонами веб-службы WCF.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Получение пакета шины обслуживания NuGet hello
Hello [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus) является hello простым способом tooget hello API служебной шины и tooconfigure приложения со всеми hello зависимости шины обслуживания. пакет NuGet tooinstall hello в своем проекте hello следующие:

1. В обозревателе решений щелкните правой кнопкой мыши **Ссылки**, затем выберите команду **Управление пакетами NuGet**.
2. Для поиска «Service Bus» и выберите hello **Microsoft Azure Service Bus** элемента. Нажмите кнопку **установить** toocomplete hello установки, а затем закройте следующие диалоговое окно приветствия:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Предоставление и использование веб-службы SOAP при использовании протокола TCP
tooexpose к существующей веб-службе WCF SOAP для внешнего использования, необходимо внести изменения toohello службы привязок и адресов. Это может потребовать изменения файла конфигурации tooyour или его могут потребовать изменений в коде, в зависимости от способа установки и настройки служб WCF. Обратите внимание, что WCF позволяет toohave несколько конечных точек сети через Здравствуйте одной службы, так можно сохранить существующие hello внутренние конечные точки при добавлении конечных точек ретрансляции для внешнего доступа к hello же время.

В этой задаче вы построить простую службу WCF и добавить tooit слушателя ретрансляции. В этом упражнении предполагается Знакомство с Visual Studio и таким образом не показывает, как все hello внутренние сведения о создании проекта. Вместо этого оно посвящено кода hello.

Прежде чем выполнять эти действия, выполните следующие процедуры tooset настройку среды hello.

1. В Visual Studio создайте консольное приложение, которое содержит два проекта «Клиент» и «Служба», в рамках решения hello.
2. Добавьте проекты tooboth пакета шины обслуживания NuGet hello. Этот пакет добавляет все проекты tooyour ссылки на необходимые сборки hello.

### <a name="how-toocreate-hello-service"></a>Как toocreate hello службы
Сначала необходимо создаете саму службу hello. Любая служба WCF состроит из трех или более различных частей.

* Определение контракта, описание того, какие сообщения передаются и операций, которые являются toobe вызывается.
* Реализация этого контракта.
* Узел, где размещена служба WCF hello и предоставляет несколько конечных точек.

Примеры кода Hello в этом разделе адресов, каждый из этих компонентов.

Hello контракт определяет одну операцию, `AddNumbers`, который складывает два числа и возвращает результат hello. Hello `IProblemSolverChannel` hello клиентского интерфейса включает toomore легко управлять временем жизни hello прокси-сервера. Рекомендуется создать этот интерфейс. Это tooput смысл этого контракта определение в отдельном файле, что этот файл можно ссылаться из проектов «Служба» и «Клиент», но можно также скопировать кода hello в обоих проектов.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

С контрактом hello в месте реализация hello выглядит следующим образом:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Программная настройка узла службы
С hello контракт и реализацию в месте теперь можно разместить службу hello. Размещение возникает внутри [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) объекта, который отвечает за управление экземплярами службы hello и конечных точек, которые прослушивает сообщения hello узлов. Hello следующий код настраивает службу hello регулярного локальную конечную точку и внешний hello tooillustrate конечную точку ретрансляции, параллельно, внутренних и внешних конечных точек. Замените строку hello *имен* с вашим именем пространства имен и *yourKey* с ключом SAS hello, полученный на предыдущем шаге установки hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

В примере hello, создайте две конечные точки, которые находятся на hello же контракта реализации. Одна из них является локальной, а вторая проецируется с помощью ретранслятора Azure. Hello основные различия между ними, hello привязки; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) для hello локальной и [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) для hello адреса конечных точек ретрансляции hello и. Hello локальная конечная точка имеет адрес локальной сети с портом distinct. Hello промежуточная конечная точка имеет адрес конечной точки, состоящие из строку hello `sb`, пространства имен и hello путь «поиск решения». Это приведет к hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, определения конечной точки службы hello как конечную точку TCP Service Bus (ретранслятор) с полным внешними именами DNS. Если нужно установить hello код, заменив заполнители hello в hello `Main` функции hello **службы** приложение будет иметь режим работы службы. Если вы хотите вашей службы toolisten исключительно на ретрансляции hello, удалите объявление hello локальную конечную точку.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Настройка узла службы в файле App.config hello
Можно также настроить hello узле, с помощью файла App.config hello. в этом случае код размещения служба Hello появляется в следующем примере hello.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

определения конечной точки Hello переместить в файл App.config hello. пакет NuGet Hello уже добавлен диапазона файла App.config toohello определений, которые являются расширениями hello необходимые конфигурации для ретрансляции Azure. Здравствуйте, следующий пример, который является hello точное эквивалент предыдущего кода hello, должны появляться непосредственно под hello **system.serviceModel** элемента. В этом примере кода предполагается, что пространство имен C# вашего проекта называется **Service**.
Замените заполнители hello ретрансляции пространства имен и ключ SAS.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

После внесения этих изменений hello служба запускается, как раньше, но с двумя конечными точками динамической: один локальный и один прослушивание в облаке hello.

### <a name="create-hello-client"></a>Создание клиента hello
#### <a name="configure-a-client-programmatically"></a>Программная настройка клиента
Служба tooconsume hello, можно создать с помощью клиента WCF [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) объекта. Служебная шина использует модель безопасности на основе маркеров, реализованную с помощью SAS. Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) класс представляет поставщик маркеров безопасности с помощью встроенных фабричные методы, которые возвращают некоторые хорошо известные поставщики токенов. Hello следующий пример использует hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) метод toohandle hello приобретения hello соответствующий маркер SAS. Hello имя и ключ, полученный из портала hello, как описано в предыдущем разделе hello.

Первый, ссылки или копировании hello `IProblemSolver` контракта в клиентский проект кода из службы hello.

Затем замените код hello в hello `Main` метод клиента hello, снова заменив замещающий текст hello ретрансляции пространства имен и ключ SAS.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Теперь можно построить hello клиент и служба hello, их запуска (запустить службу hello сначала), и клиент hello вызывает службу hello и печатает **9**. Hello клиента и сервера можно запускать на различных компьютерах, даже в сетях и hello связи по-прежнему будет работать. Hello клиентский код может выполнять в облаке hello или локально.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Настройка клиента в файле App.config hello
Hello, следующий код показывает, как tooconfigure hello клиента с помощью hello файл App.config.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

определения конечной точки Hello переместить в файл App.config hello. Hello следующий пример, который является hello совпадает с перечисленными выше кода hello, должны появляться непосредственно под hello `<system.serviceModel>` элемента. Здесь как и ранее, необходимо заменить заполнители hello ретрансляции пространства имен и ключ SAS.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello Azure ретрансляции, выполните следующие дополнительные toolearn ссылки.

* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Обзор архитектуры служебной шины Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Загрузить образцы Service Bus [Azure образцы] [ Azure samples] или разделе hello [обзор примеров Service Bus][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
