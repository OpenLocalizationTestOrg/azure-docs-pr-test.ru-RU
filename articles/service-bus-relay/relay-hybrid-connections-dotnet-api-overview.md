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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Обзор API-интерфейсов гибридных подключений ретранслятора Azure для платформы .NET Standard

В этой статье приведена сводка hello ключа гибридного подключения Azure ретрансляции .NET Standard [клиентские API](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Построитель строк подключения ретранслятора

Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] класс форматы строк подключения, определенные tooRelay гибридных подключений. Его можно использовать tooverify hello формат строки подключения или toobuild строку подключения с нуля. В разделе hello, следующий код, например:

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

Соединение можно также передать строку непосредственно toohello `RelayConnectionStringBuilder` метод. Эта операция включает tooverify, строка подключения hello в допустимом формате. Если любой из параметров hello являются недействительными, конструктор hello приводит к возникновению ошибки `ArgumentException`.

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

## <a name="hybrid-connection-stream"></a>Поток гибридного подключения
Hello [HybridConnectionStream] [ HCStream] класс toosend основной объект, используемый hello и получать данные из конечной точки ретрансляции Azure ли вы работаете с [HybridConnectionClient] [ HCClient], или [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Получение потока гибридного подключения

#### <a name="listener"></a>Прослушиватель
С помощью [HybridConnectionListener][HCListener] можно получить объект `HybridConnectionStream` следующим образом:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Клиент
С помощью [HybridConnectionClient][HCClient] можно получить объект `HybridConnectionStream` следующим образом:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Получение данных
Hello [HybridConnectionStream] [ HCStream] класс позволяет осуществлять двустороннее взаимодействие. В большинстве случаев постоянно получать из потока hello. При чтении из потока hello текста, вы также можете toouse [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) объекта, который позволяет упростить анализ данных hello. Например, можно считывать данные как текст, а не как `byte[]`.

Hello следующий код считывает отдельные строки текста из потока hello до запроса отмены:

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

### <a name="sending-data"></a>Отправка данных
После установления соединения, можно отправить сообщение toohello промежуточную конечную точку. Поскольку объект подключения hello наследует [поток](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), отправка данных в качестве `byte[]`. Следующий пример показывает как Hello toodo это:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Тем не менее, если требуется текст toosend напрямую, без необходимости каждый раз, строка hello tooencode можно заключить hello `hybridConnectionStream` объекта с [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) объекта.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:

* [Microsoft.Azure.Relay Namespace](/dotnet/api/microsoft.azure.relay) (Пространство имен Microsoft.Azure.Relay)
* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Available Relay APIs](relay-api-overview.md) (Доступные API-интерфейсы ретранслятора)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener