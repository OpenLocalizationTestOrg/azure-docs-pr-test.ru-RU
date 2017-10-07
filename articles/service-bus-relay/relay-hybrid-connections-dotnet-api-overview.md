---
title: "aaaOverview из hello Azure ретрансляции стандартные API-интерфейсы .NET | Документы Microsoft"
description: "Обзор API-интерфейсов ретранслятора для платформы .NET Standard"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="4fb7a-103">Обзор API-интерфейсов гибридных подключений ретранслятора Azure для платформы .NET Standard</span><span class="sxs-lookup"><span data-stu-id="4fb7a-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="4fb7a-104">В этой статье приведена сводка hello ключа гибридного подключения Azure ретрансляции .NET Standard [клиентские API](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="4fb7a-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="4fb7a-105">Построитель строк подключения ретранслятора</span><span class="sxs-lookup"><span data-stu-id="4fb7a-105">Relay Connection String Builder</span></span>

<span data-ttu-id="4fb7a-106">Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] класс форматы строк подключения, определенные tooRelay гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="4fb7a-107">Его можно использовать tooverify hello формат строки подключения или toobuild строку подключения с нуля.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="4fb7a-108">В разделе hello, следующий код, например:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-108">See hello following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

<span data-ttu-id="4fb7a-109">Соединение можно также передать строку непосредственно toohello `RelayConnectionStringBuilder` метод.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="4fb7a-110">Эта операция включает tooverify, строка подключения hello в допустимом формате.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="4fb7a-111">Если любой из параметров hello являются недействительными, конструктор hello приводит к возникновению ошибки `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="4fb7a-112">Поток гибридного подключения</span><span class="sxs-lookup"><span data-stu-id="4fb7a-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="4fb7a-113">Hello [HybridConnectionStream] [ HCStream] класс toosend основной объект, используемый hello и получать данные из конечной точки ретрансляции Azure ли вы работаете с [HybridConnectionClient] [ HCClient], или [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="4fb7a-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="4fb7a-114">Получение потока гибридного подключения</span><span class="sxs-lookup"><span data-stu-id="4fb7a-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="4fb7a-115">Прослушиватель</span><span class="sxs-lookup"><span data-stu-id="4fb7a-115">Listener</span></span>
<span data-ttu-id="4fb7a-116">С помощью [HybridConnectionListener][HCListener] можно получить объект `HybridConnectionStream` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="4fb7a-117">Клиент</span><span class="sxs-lookup"><span data-stu-id="4fb7a-117">Client</span></span>
<span data-ttu-id="4fb7a-118">С помощью [HybridConnectionClient][HCClient] можно получить объект `HybridConnectionStream` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="4fb7a-119">Получение данных</span><span class="sxs-lookup"><span data-stu-id="4fb7a-119">Receiving data</span></span>
<span data-ttu-id="4fb7a-120">Hello [HybridConnectionStream] [ HCStream] класс позволяет осуществлять двустороннее взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="4fb7a-121">В большинстве случаев постоянно получать из потока hello.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="4fb7a-122">При чтении из потока hello текста, вы также можете toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) объекта, который позволяет упростить анализ данных hello.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="4fb7a-123">Например, можно считывать данные как текст, а не как `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="4fb7a-124">Hello следующий код считывает отдельные строки текста из потока hello до запроса отмены:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="4fb7a-125">Отправка данных</span><span class="sxs-lookup"><span data-stu-id="4fb7a-125">Sending data</span></span>
<span data-ttu-id="4fb7a-126">После установления соединения, можно отправить сообщение toohello промежуточную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="4fb7a-127">Поскольку объект подключения hello наследует [поток](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), отправка данных в качестве `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="4fb7a-128">Следующий пример показывает как Hello toodo это:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="4fb7a-129">Тем не менее, если требуется текст toosend напрямую, без необходимости каждый раз, строка hello tooencode можно заключить hello `hybridConnectionStream` объекта с [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="4fb7a-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="4fb7a-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fb7a-130">Next steps</span></span>
<span data-ttu-id="4fb7a-131">toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="4fb7a-131">toolearn more about Azure Relay, visit these links:</span></span>

* <span data-ttu-id="4fb7a-132">[Microsoft.Azure.Relay Namespace](/dotnet/api/microsoft.azure.relay) (Пространство имен Microsoft.Azure.Relay)</span><span class="sxs-lookup"><span data-stu-id="4fb7a-132">[Microsoft.Azure.Relay reference](/dotnet/api/microsoft.azure.relay)</span></span>
* [<span data-ttu-id="4fb7a-133">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="4fb7a-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* <span data-ttu-id="4fb7a-134">[Available Relay APIs](relay-api-overview.md) (Доступные API-интерфейсы ретранслятора)</span><span class="sxs-lookup"><span data-stu-id="4fb7a-134">[Available Relay APIs](relay-api-overview.md)</span></span>

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener