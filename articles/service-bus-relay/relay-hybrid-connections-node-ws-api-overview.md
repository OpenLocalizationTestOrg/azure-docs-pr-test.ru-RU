---
title: "aaaOverview из API-интерфейсов узла Azure ретрансляции hello | Документы Microsoft"
description: "Общие сведения об API узла ретранслятора"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="f6246-103">Общие сведения об API узла гибридных подключений ретранслятора</span><span class="sxs-lookup"><span data-stu-id="f6246-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="f6246-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f6246-104">Overview</span></span>

<span data-ttu-id="f6246-105">Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) основаны на узел пакета для гибридных подключений ретрансляции Azure и расширяет hello [«ws»](https://www.npmjs.com/package/ws) пакета NPM.</span><span class="sxs-lookup"><span data-stu-id="f6246-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="f6246-106">Этот пакет повторно экспортирует все экспорты, базовый пакет и добавляет новый экспорты, которые обеспечивают интеграцию с функцией гибридных подключений службы ретрансляции Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6246-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="f6246-107">Существующие приложения, `require('ws')` можно использовать данный пакет `require('hyco-ws')` вместо этого, который также позволяет гибридные сценарии, в которых приложение может прослушивать соединения WebSocket локально из «внутри брандмауэра hello» и с помощью гибридных подключений все на Здравствуйте же время.</span><span class="sxs-lookup"><span data-stu-id="f6246-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="f6246-108">Документация</span><span class="sxs-lookup"><span data-stu-id="f6246-108">Documentation</span></span>

<span data-ttu-id="f6246-109">Hello API-интерфейсы являются [задокументированы в пакете главной «ws» hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="f6246-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="f6246-110">В этой статье описаны отличия этого пакета от базового.</span><span class="sxs-lookup"><span data-stu-id="f6246-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="f6246-111">Hello основные различия между hello базовый пакет и этот «hyco-ws» то, что он добавляет новый класс server экспортировать через `require('hyco-ws').RelayedServer`и несколько вспомогательных методов.</span><span class="sxs-lookup"><span data-stu-id="f6246-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="f6246-112">Вспомогательные методы пакета</span><span class="sxs-lookup"><span data-stu-id="f6246-112">Package helper methods</span></span>

<span data-ttu-id="f6246-113">Доступны несколько служебных методов во время экспорта пакета hello, на которую ссылается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f6246-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="f6246-114">Hello вспомогательные методы предназначены для использования с этим пакетом, но также может использоваться сервером узла для включения веб- или устройство прослушиватели toocreate клиентов или отправителей.</span><span class="sxs-lookup"><span data-stu-id="f6246-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="f6246-115">Hello сервер использует эти методы, передав их в URI, которые внедрить кратковременных маркеры.</span><span class="sxs-lookup"><span data-stu-id="f6246-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="f6246-116">Эти URI также можно с помощью общих стеков WebSocket, не поддерживающих задания заголовков HTTP для подтверждения hello WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f6246-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="f6246-117">Внедрение маркерах авторизации в hello URI поддерживается в основном для этих сценариев использования внешнего библиотеки.</span><span class="sxs-lookup"><span data-stu-id="f6246-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="f6246-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="f6246-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="f6246-119">Создает допустимый Azure ретрансляции гибридное подключение прослушиватель URI для hello заданным пространством имен и путь.</span><span class="sxs-lookup"><span data-stu-id="f6246-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="f6246-120">Затем этот URI можно использовать с версией ретрансляции hello hello WebSocketServer класса.</span><span class="sxs-lookup"><span data-stu-id="f6246-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="f6246-121">`namespaceName`(обязательно) — hello доменном имя пространства имен toouse hello Azure ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="f6246-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="f6246-122">`path`(обязательно) — hello имя существующего соединения гибридной Azure ретрансляции в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="f6246-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="f6246-123">`token`(необязательно) — доступ к ранее выданных ретрансляции маркер, который внедряется в прослушивателе hello URI (см. следующий пример hello).</span><span class="sxs-lookup"><span data-stu-id="f6246-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="f6246-124">`id` (необязательно) — идентификатор отслеживания, который позволяет отслеживать комплексную диагностику запросов.</span><span class="sxs-lookup"><span data-stu-id="f6246-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="f6246-125">Hello `token` значение является необязательным и должен использоваться только в случае заголовки можно toosend HTTP вместе с подтверждения WebSocket hello, как случае hello со стеком hello W3C WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f6246-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="f6246-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="f6246-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="f6246-127">Создает допустимый Azure ретрансляции гибридного подключения send URI для hello заданным пространством имен и путь.</span><span class="sxs-lookup"><span data-stu-id="f6246-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="f6246-128">Этот URI можно использовать с любым клиентом WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f6246-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="f6246-129">`namespaceName`(обязательно) — hello доменном имя пространства имен toouse hello Azure ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="f6246-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="f6246-130">`path`(обязательно) — hello имя существующего соединения гибридной Azure ретрансляции в этом пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="f6246-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="f6246-131">`token`(необязательно) — ранее выданного токена доступа к ретрансляции, внедренных в hello отправки URI (см. следующий пример hello).</span><span class="sxs-lookup"><span data-stu-id="f6246-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="f6246-132">`id` (необязательно) — идентификатор отслеживания, который позволяет отслеживать комплексную диагностику запросов.</span><span class="sxs-lookup"><span data-stu-id="f6246-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="f6246-133">Hello `token` значение является необязательным и должен использоваться только в случае заголовки можно toosend HTTP вместе с подтверждения WebSocket hello, как случае hello со стеком hello W3C WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f6246-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="f6246-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="f6246-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="f6246-135">Создает маркер Azure ретрансляции общего доступа подписи (SAS) для hello заданный универсальный код Ресурса, правила SAS и ключа SAS правила, допустимый для hello даны количество секунд или часа hello в текущий момент Если hello срока действия аргумент указан.</span><span class="sxs-lookup"><span data-stu-id="f6246-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="f6246-136">`uri`(обязательно) — hello для какой hello маркер является toobe выданный URI.</span><span class="sxs-lookup"><span data-stu-id="f6246-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="f6246-137">Hello URI является схему HTTP нормализованный toouse hello и удаляются данные строки запроса.</span><span class="sxs-lookup"><span data-stu-id="f6246-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="f6246-138">`ruleName`(обязательно) — имя для сущности либо hello, представленного заданным URI hello правила SAS или для приветствия имен обозначаются hello часть URI узла.</span><span class="sxs-lookup"><span data-stu-id="f6246-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="f6246-139">`key`(обязательно) — допустимый ключ для правила SAS hello.</span><span class="sxs-lookup"><span data-stu-id="f6246-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="f6246-140">`expirationSeconds`(необязательно) — hello количество секунд до hello созданный маркер следует срока действия.</span><span class="sxs-lookup"><span data-stu-id="f6246-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="f6246-141">Если не указано, по умолчанию hello составляет 1 час (3600).</span><span class="sxs-lookup"><span data-stu-id="f6246-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="f6246-142">Hello выданный маркер предоставляет hello права, связанные с hello указанного правила SAS для hello учетом длительности.</span><span class="sxs-lookup"><span data-stu-id="f6246-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="f6246-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="f6246-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="f6246-144">Этот метод является функциональным эквивалентом toohello `createRelayToken` метод задокументированных, но возвращает hello маркера правильно присоединенных toohello входной URI.</span><span class="sxs-lookup"><span data-stu-id="f6246-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="f6246-145">Класс ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="f6246-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="f6246-146">Hello `hycows.RelayedServer` класс является альтернативным toohello `ws.Server` класс, который не прослушивает hello локальной сети, но делегирует прослушивания toohello служба ретрансляции Azure.</span><span class="sxs-lookup"><span data-stu-id="f6246-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="f6246-147">Hello двух классов, большей части совместимы, это значит, что существующие приложения с помощью hello контракта `ws.Server` класс легко может достичь измененные toouse hello ретрансляцией версии.</span><span class="sxs-lookup"><span data-stu-id="f6246-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="f6246-148">Ниже перечислены основные различия Hello в конструктор hello и доступных параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="f6246-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="f6246-149">Конструктор</span><span class="sxs-lookup"><span data-stu-id="f6246-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="f6246-150">Hello `RelayedServer` конструктор поддерживает набор аргументов, чем hello `Server`, так как он не прослушивателя автономный или может toobe, внедренный в это существующая платформа прослушивателя HTTP.</span><span class="sxs-lookup"><span data-stu-id="f6246-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="f6246-151">Доступны также меньше возможностей с момента hello WebSocket управления является главным образом делегированного toohello служба ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="f6246-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="f6246-152">Аргументы конструктора:</span><span class="sxs-lookup"><span data-stu-id="f6246-152">Constructor arguments:</span></span>

- <span data-ttu-id="f6246-153">`server`(обязательно) — hello полным URI для имя гибридного подключения на какие toolisten обычно создается с hello WebSocket.createRelayListenUri() вспомогательный метод.</span><span class="sxs-lookup"><span data-stu-id="f6246-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="f6246-154">`token`(обязательно) — этот аргумент содержит строку ранее выданных маркеров или функции обратного вызова, который может быть вызван tooobtain маркера строки.</span><span class="sxs-lookup"><span data-stu-id="f6246-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="f6246-155">параметр обратного вызова Hello предпочтителен, как позволяет обновления маркеров.</span><span class="sxs-lookup"><span data-stu-id="f6246-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="f6246-156">События</span><span class="sxs-lookup"><span data-stu-id="f6246-156">Events</span></span>

<span data-ttu-id="f6246-157">`RelayedServer`экземпляры выдавать три события, которые включать вы toohandle входящие запросы, подключения и обнаружить условия ошибки.</span><span class="sxs-lookup"><span data-stu-id="f6246-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="f6246-158">Необходимо подписаться toohello `connect` toohandle сообщения о событиях.</span><span class="sxs-lookup"><span data-stu-id="f6246-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="f6246-159">headers</span><span class="sxs-lookup"><span data-stu-id="f6246-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="f6246-160">Hello `headers` событие возникает непосредственно перед принимается входящего подключения, включение изменения hello заголовки toosend toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="f6246-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="f6246-161">connection;</span><span class="sxs-lookup"><span data-stu-id="f6246-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="f6246-162">Генерируется, когда принимается новое подключение WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f6246-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="f6246-163">Hello объект имеет тип `ws.WebSocket`, совпадает с базовым пакетом hello.</span><span class="sxs-lookup"><span data-stu-id="f6246-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="f6246-164">error</span><span class="sxs-lookup"><span data-stu-id="f6246-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="f6246-165">Если основной сервер hello выдает ошибку, он перенаправляется здесь.</span><span class="sxs-lookup"><span data-stu-id="f6246-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="f6246-166">Вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="f6246-166">Helpers</span></span>

<span data-ttu-id="f6246-167">Запуск toosimplify ретранслироваться сервера и немедленно подписка подключений tooincoming hello пакет предоставляет простой вспомогательную функцию, который также используется в примерах hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f6246-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="f6246-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="f6246-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="f6246-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="f6246-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="f6246-170">Этот метод вызывает конструктор toocreate hello новый экземпляр hello RelayedServer и затем подписывается на событие toohello «подключения» указано hello обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f6246-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="f6246-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="f6246-171">relayedConnect</span></span>

<span data-ttu-id="f6246-172">Просто зеркального отображения hello `createRelayedServer` вспомогательные функции, `relayedConnect` создает подключение клиента и подписывается на событие «открыто» toohello полученный сокете hello.</span><span class="sxs-lookup"><span data-stu-id="f6246-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="f6246-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6246-173">Next steps</span></span>
<span data-ttu-id="f6246-174">toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f6246-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="f6246-175">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="f6246-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* <span data-ttu-id="f6246-176">[Available Relay APIs](relay-api-overview.md) (Доступные API-интерфейсы ретранслятора)</span><span class="sxs-lookup"><span data-stu-id="f6246-176">[Available Relay APIs](relay-api-overview.md)</span></span>
