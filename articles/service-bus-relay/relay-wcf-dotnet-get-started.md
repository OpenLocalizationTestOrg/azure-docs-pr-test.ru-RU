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
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="9dd53-103">Как toouse Azure ретрансляции WCF ретрансляций с .NET</span><span class="sxs-lookup"><span data-stu-id="9dd53-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="9dd53-104">В этой статье описывается, как toouse hello служба ретрансляции Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd53-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="9dd53-105">Hello примеры написаны на C# и использовать API Windows Communication Foundation (WCF) hello с расширениями, содержащихся в hello сборки служебной шины.</span><span class="sxs-lookup"><span data-stu-id="9dd53-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="9dd53-106">Дополнительные сведения о Azure ретрансляции см. в разделе hello [Обзор Azure ретрансляции](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="9dd53-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="9dd53-107">Что такое ретранслятор WCF?</span><span class="sxs-lookup"><span data-stu-id="9dd53-107">What is WCF Relay?</span></span>

<span data-ttu-id="9dd53-108">Hello Azure [ *ретрансляции WCF* ](relay-what-is-it.md) служба позволяет toobuild гибридных приложений, которые запускаются в центре обработки данных Azure и среде предприятия в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="9dd53-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="9dd53-109">служба ретрансляции Hello облегчает это, позволяя toosecurely предоставлять службы Windows Communication Foundation (WCF), которые находятся в корпоративной среде организации сети toohello общедоступное облако, без необходимости tooopen подключения брандмауэра или требования Инфраструктура корпоративной сети tooa влияние изменений.</span><span class="sxs-lookup"><span data-stu-id="9dd53-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Обзор ретранслятора WCF](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="9dd53-111">Ретранслятор Azure позволяет toohost служб WCF в существующей среде предприятия.</span><span class="sxs-lookup"><span data-stu-id="9dd53-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="9dd53-112">Затем можно делегировать прослушивание входящих сеансов и запросов toothese WCF toohello ретрансляции службы, запущенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd53-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="9dd53-113">Благодаря этому вы tooexpose эти службы tooapplication код, выполняющийся в Azure, или toomobile работников или экстрасети партнера сред.</span><span class="sxs-lookup"><span data-stu-id="9dd53-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="9dd53-114">Ретрансляции позволяет toosecurely контролировать, кто может обращаться к службам на уровне детально.</span><span class="sxs-lookup"><span data-stu-id="9dd53-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="9dd53-115">Она обеспечивает функциональные возможности приложений tooexpose мощные и безопасный способ и данных из существующих решений и использовать преимущества ее из облака hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="9dd53-116">Здесь рассматривается как toocreate toouse ретрансляции Azure предоставляется с помощью привязки канала TCP, который реализует безопасного обмена данными между двумя сторонами веб-службы WCF.</span><span class="sxs-lookup"><span data-stu-id="9dd53-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="9dd53-117">Получение пакета шины обслуживания NuGet hello</span><span class="sxs-lookup"><span data-stu-id="9dd53-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="9dd53-118">Hello [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus) является hello простым способом tooget hello API служебной шины и tooconfigure приложения со всеми hello зависимости шины обслуживания.</span><span class="sxs-lookup"><span data-stu-id="9dd53-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="9dd53-119">пакет NuGet tooinstall hello в своем проекте hello следующие:</span><span class="sxs-lookup"><span data-stu-id="9dd53-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="9dd53-120">В обозревателе решений щелкните правой кнопкой мыши **Ссылки**, затем выберите команду **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="9dd53-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="9dd53-121">Для поиска «Service Bus» и выберите hello **Microsoft Azure Service Bus** элемента.</span><span class="sxs-lookup"><span data-stu-id="9dd53-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="9dd53-122">Нажмите кнопку **установить** toocomplete hello установки, а затем закройте следующие диалоговое окно приветствия:</span><span class="sxs-lookup"><span data-stu-id="9dd53-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="9dd53-123">Предоставление и использование веб-службы SOAP при использовании протокола TCP</span><span class="sxs-lookup"><span data-stu-id="9dd53-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="9dd53-124">tooexpose к существующей веб-службе WCF SOAP для внешнего использования, необходимо внести изменения toohello службы привязок и адресов.</span><span class="sxs-lookup"><span data-stu-id="9dd53-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="9dd53-125">Это может потребовать изменения файла конфигурации tooyour или его могут потребовать изменений в коде, в зависимости от способа установки и настройки служб WCF.</span><span class="sxs-lookup"><span data-stu-id="9dd53-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="9dd53-126">Обратите внимание, что WCF позволяет toohave несколько конечных точек сети через Здравствуйте одной службы, так можно сохранить существующие hello внутренние конечные точки при добавлении конечных точек ретрансляции для внешнего доступа к hello же время.</span><span class="sxs-lookup"><span data-stu-id="9dd53-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="9dd53-127">В этой задаче вы построить простую службу WCF и добавить tooit слушателя ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="9dd53-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="9dd53-128">В этом упражнении предполагается Знакомство с Visual Studio и таким образом не показывает, как все hello внутренние сведения о создании проекта.</span><span class="sxs-lookup"><span data-stu-id="9dd53-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="9dd53-129">Вместо этого оно посвящено кода hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="9dd53-130">Прежде чем выполнять эти действия, выполните следующие процедуры tooset настройку среды hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="9dd53-131">В Visual Studio создайте консольное приложение, которое содержит два проекта «Клиент» и «Служба», в рамках решения hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="9dd53-132">Добавьте проекты tooboth пакета шины обслуживания NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="9dd53-133">Этот пакет добавляет все проекты tooyour ссылки на необходимые сборки hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="9dd53-134">Как toocreate hello службы</span><span class="sxs-lookup"><span data-stu-id="9dd53-134">How toocreate hello service</span></span>
<span data-ttu-id="9dd53-135">Сначала необходимо создаете саму службу hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-135">First, create hello service itself.</span></span> <span data-ttu-id="9dd53-136">Любая служба WCF состроит из трех или более различных частей.</span><span class="sxs-lookup"><span data-stu-id="9dd53-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="9dd53-137">Определение контракта, описание того, какие сообщения передаются и операций, которые являются toobe вызывается.</span><span class="sxs-lookup"><span data-stu-id="9dd53-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="9dd53-138">Реализация этого контракта.</span><span class="sxs-lookup"><span data-stu-id="9dd53-138">Implementation of that contract.</span></span>
* <span data-ttu-id="9dd53-139">Узел, где размещена служба WCF hello и предоставляет несколько конечных точек.</span><span class="sxs-lookup"><span data-stu-id="9dd53-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="9dd53-140">Примеры кода Hello в этом разделе адресов, каждый из этих компонентов.</span><span class="sxs-lookup"><span data-stu-id="9dd53-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="9dd53-141">Hello контракт определяет одну операцию, `AddNumbers`, который складывает два числа и возвращает результат hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="9dd53-142">Hello `IProblemSolverChannel` hello клиентского интерфейса включает toomore легко управлять временем жизни hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="9dd53-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="9dd53-143">Рекомендуется создать этот интерфейс.</span><span class="sxs-lookup"><span data-stu-id="9dd53-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="9dd53-144">Это tooput смысл этого контракта определение в отдельном файле, что этот файл можно ссылаться из проектов «Служба» и «Клиент», но можно также скопировать кода hello в обоих проектов.</span><span class="sxs-lookup"><span data-stu-id="9dd53-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

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

<span data-ttu-id="9dd53-145">С контрактом hello в месте реализация hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dd53-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="9dd53-146">Программная настройка узла службы</span><span class="sxs-lookup"><span data-stu-id="9dd53-146">Configure a service host programmatically</span></span>
<span data-ttu-id="9dd53-147">С hello контракт и реализацию в месте теперь можно разместить службу hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="9dd53-148">Размещение возникает внутри [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) объекта, который отвечает за управление экземплярами службы hello и конечных точек, которые прослушивает сообщения hello узлов.</span><span class="sxs-lookup"><span data-stu-id="9dd53-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="9dd53-149">Hello следующий код настраивает службу hello регулярного локальную конечную точку и внешний hello tooillustrate конечную точку ретрансляции, параллельно, внутренних и внешних конечных точек.</span><span class="sxs-lookup"><span data-stu-id="9dd53-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="9dd53-150">Замените строку hello *имен* с вашим именем пространства имен и *yourKey* с ключом SAS hello, полученный на предыдущем шаге установки hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

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

<span data-ttu-id="9dd53-151">В примере hello, создайте две конечные точки, которые находятся на hello же контракта реализации.</span><span class="sxs-lookup"><span data-stu-id="9dd53-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="9dd53-152">Одна из них является локальной, а вторая проецируется с помощью ретранслятора Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd53-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="9dd53-153">Hello основные различия между ними, hello привязки; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) для hello локальной и [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) для hello адреса конечных точек ретрансляции hello и.</span><span class="sxs-lookup"><span data-stu-id="9dd53-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="9dd53-154">Hello локальная конечная точка имеет адрес локальной сети с портом distinct.</span><span class="sxs-lookup"><span data-stu-id="9dd53-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="9dd53-155">Hello промежуточная конечная точка имеет адрес конечной точки, состоящие из строку hello `sb`, пространства имен и hello путь «поиск решения».</span><span class="sxs-lookup"><span data-stu-id="9dd53-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="9dd53-156">Это приведет к hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, определения конечной точки службы hello как конечную точку TCP Service Bus (ретранслятор) с полным внешними именами DNS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="9dd53-157">Если нужно установить hello код, заменив заполнители hello в hello `Main` функции hello **службы** приложение будет иметь режим работы службы.</span><span class="sxs-lookup"><span data-stu-id="9dd53-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="9dd53-158">Если вы хотите вашей службы toolisten исключительно на ретрансляции hello, удалите объявление hello локальную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="9dd53-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="9dd53-159">Настройка узла службы в файле App.config hello</span><span class="sxs-lookup"><span data-stu-id="9dd53-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="9dd53-160">Можно также настроить hello узле, с помощью файла App.config hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="9dd53-161">в этом случае код размещения служба Hello появляется в следующем примере hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="9dd53-162">определения конечной точки Hello переместить в файл App.config hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="9dd53-163">пакет NuGet Hello уже добавлен диапазона файла App.config toohello определений, которые являются расширениями hello необходимые конфигурации для ретрансляции Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd53-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="9dd53-164">Здравствуйте, следующий пример, который является hello точное эквивалент предыдущего кода hello, должны появляться непосредственно под hello **system.serviceModel** элемента.</span><span class="sxs-lookup"><span data-stu-id="9dd53-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="9dd53-165">В этом примере кода предполагается, что пространство имен C# вашего проекта называется **Service**.</span><span class="sxs-lookup"><span data-stu-id="9dd53-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="9dd53-166">Замените заполнители hello ретрансляции пространства имен и ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="9dd53-167">После внесения этих изменений hello служба запускается, как раньше, но с двумя конечными точками динамической: один локальный и один прослушивание в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="9dd53-168">Создание клиента hello</span><span class="sxs-lookup"><span data-stu-id="9dd53-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="9dd53-169">Программная настройка клиента</span><span class="sxs-lookup"><span data-stu-id="9dd53-169">Configure a client programmatically</span></span>
<span data-ttu-id="9dd53-170">Служба tooconsume hello, можно создать с помощью клиента WCF [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="9dd53-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="9dd53-171">Служебная шина использует модель безопасности на основе маркеров, реализованную с помощью SAS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="9dd53-172">Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) класс представляет поставщик маркеров безопасности с помощью встроенных фабричные методы, которые возвращают некоторые хорошо известные поставщики токенов.</span><span class="sxs-lookup"><span data-stu-id="9dd53-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="9dd53-173">Hello следующий пример использует hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) метод toohandle hello приобретения hello соответствующий маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="9dd53-174">Hello имя и ключ, полученный из портала hello, как описано в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="9dd53-175">Первый, ссылки или копировании hello `IProblemSolver` контракта в клиентский проект кода из службы hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="9dd53-176">Затем замените код hello в hello `Main` метод клиента hello, снова заменив замещающий текст hello ретрансляции пространства имен и ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="9dd53-177">Теперь можно построить hello клиент и служба hello, их запуска (запустить службу hello сначала), и клиент hello вызывает службу hello и печатает **9**.</span><span class="sxs-lookup"><span data-stu-id="9dd53-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="9dd53-178">Hello клиента и сервера можно запускать на различных компьютерах, даже в сетях и hello связи по-прежнему будет работать.</span><span class="sxs-lookup"><span data-stu-id="9dd53-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="9dd53-179">Hello клиентский код может выполнять в облаке hello или локально.</span><span class="sxs-lookup"><span data-stu-id="9dd53-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="9dd53-180">Настройка клиента в файле App.config hello</span><span class="sxs-lookup"><span data-stu-id="9dd53-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="9dd53-181">Hello, следующий код показывает, как tooconfigure hello клиента с помощью hello файл App.config.</span><span class="sxs-lookup"><span data-stu-id="9dd53-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="9dd53-182">определения конечной точки Hello переместить в файл App.config hello.</span><span class="sxs-lookup"><span data-stu-id="9dd53-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="9dd53-183">Hello следующий пример, который является hello совпадает с перечисленными выше кода hello, должны появляться непосредственно под hello `<system.serviceModel>` элемента.</span><span class="sxs-lookup"><span data-stu-id="9dd53-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="9dd53-184">Здесь как и ранее, необходимо заменить заполнители hello ретрансляции пространства имен и ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="9dd53-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9dd53-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dd53-185">Next steps</span></span>
<span data-ttu-id="9dd53-186">Теперь, когда вы узнали основы hello Azure ретрансляции, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="9dd53-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="9dd53-187">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="9dd53-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="9dd53-188">Обзор архитектуры служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="9dd53-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="9dd53-189">Загрузить образцы Service Bus [Azure образцы] [ Azure samples] или разделе hello [обзор примеров Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="9dd53-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
