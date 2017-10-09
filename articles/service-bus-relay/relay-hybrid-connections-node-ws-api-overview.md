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
# <a name="relay-hybrid-connections-node-api-overview"></a>Общие сведения об API узла гибридных подключений ретранслятора

## <a name="overview"></a>Обзор

Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) основаны на узел пакета для гибридных подключений ретрансляции Azure и расширяет hello [«ws»](https://www.npmjs.com/package/ws) пакета NPM. Этот пакет повторно экспортирует все экспорты, базовый пакет и добавляет новый экспорты, которые обеспечивают интеграцию с функцией гибридных подключений службы ретрансляции Azure hello. 

Существующие приложения, `require('ws')` можно использовать данный пакет `require('hyco-ws')` вместо этого, который также позволяет гибридные сценарии, в которых приложение может прослушивать соединения WebSocket локально из «внутри брандмауэра hello» и с помощью гибридных подключений все на Здравствуйте же время.
  
## <a name="documentation"></a>Документация

Hello API-интерфейсы являются [задокументированы в пакете главной «ws» hello](https://github.com/websockets/ws/blob/master/doc/ws.md). В этой статье описаны отличия этого пакета от базового. 

Hello основные различия между hello базовый пакет и этот «hyco-ws» то, что он добавляет новый класс server экспортировать через `require('hyco-ws').RelayedServer`и несколько вспомогательных методов.

### <a name="package-helper-methods"></a>Вспомогательные методы пакета

Доступны несколько служебных методов во время экспорта пакета hello, на которую ссылается следующим образом:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

Hello вспомогательные методы предназначены для использования с этим пакетом, но также может использоваться сервером узла для включения веб- или устройство прослушиватели toocreate клиентов или отправителей. Hello сервер использует эти методы, передав их в URI, которые внедрить кратковременных маркеры. Эти URI также можно с помощью общих стеков WebSocket, не поддерживающих задания заголовков HTTP для подтверждения hello WebSocket. Внедрение маркерах авторизации в hello URI поддерживается в основном для этих сценариев использования внешнего библиотеки. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Создает допустимый Azure ретрансляции гибридное подключение прослушиватель URI для hello заданным пространством имен и путь. Затем этот URI можно использовать с версией ретрансляции hello hello WebSocketServer класса.

- `namespaceName`(обязательно) — hello доменном имя пространства имен toouse hello Azure ретрансляции.
- `path`(обязательно) — hello имя существующего соединения гибридной Azure ретрансляции в этом пространстве имен.
- `token`(необязательно) — доступ к ранее выданных ретрансляции маркер, который внедряется в прослушивателе hello URI (см. следующий пример hello).
- `id` (необязательно) — идентификатор отслеживания, который позволяет отслеживать комплексную диагностику запросов.

Hello `token` значение является необязательным и должен использоваться только в случае заголовки можно toosend HTTP вместе с подтверждения WebSocket hello, как случае hello со стеком hello W3C WebSocket.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Создает допустимый Azure ретрансляции гибридного подключения send URI для hello заданным пространством имен и путь. Этот URI можно использовать с любым клиентом WebSocket.

- `namespaceName`(обязательно) — hello доменном имя пространства имен toouse hello Azure ретрансляции.
- `path`(обязательно) — hello имя существующего соединения гибридной Azure ретрансляции в этом пространстве имен.
- `token`(необязательно) — ранее выданного токена доступа к ретрансляции, внедренных в hello отправки URI (см. следующий пример hello).
- `id` (необязательно) — идентификатор отслеживания, который позволяет отслеживать комплексную диагностику запросов.

Hello `token` значение является необязательным и должен использоваться только в случае заголовки можно toosend HTTP вместе с подтверждения WebSocket hello, как случае hello со стеком hello W3C WebSocket.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Создает маркер Azure ретрансляции общего доступа подписи (SAS) для hello заданный универсальный код Ресурса, правила SAS и ключа SAS правила, допустимый для hello даны количество секунд или часа hello в текущий момент Если hello срока действия аргумент указан.

- `uri`(обязательно) — hello для какой hello маркер является toobe выданный URI. Hello URI является схему HTTP нормализованный toouse hello и удаляются данные строки запроса.
- `ruleName`(обязательно) — имя для сущности либо hello, представленного заданным URI hello правила SAS или для приветствия имен обозначаются hello часть URI узла.
- `key`(обязательно) — допустимый ключ для правила SAS hello. 
- `expirationSeconds`(необязательно) — hello количество секунд до hello созданный маркер следует срока действия. Если не указано, по умолчанию hello составляет 1 час (3600).

Hello выданный маркер предоставляет hello права, связанные с hello указанного правила SAS для hello учетом длительности.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Этот метод является функциональным эквивалентом toohello `createRelayToken` метод задокументированных, но возвращает hello маркера правильно присоединенных toohello входной URI.

### <a name="class-wsrelayedserver"></a>Класс ws.RelayedServer

Hello `hycows.RelayedServer` класс является альтернативным toohello `ws.Server` класс, который не прослушивает hello локальной сети, но делегирует прослушивания toohello служба ретрансляции Azure.

Hello двух классов, большей части совместимы, это значит, что существующие приложения с помощью hello контракта `ws.Server` класс легко может достичь измененные toouse hello ретрансляцией версии. Ниже перечислены основные различия Hello в конструктор hello и доступных параметрах hello.

#### <a name="constructor"></a>Конструктор  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Hello `RelayedServer` конструктор поддерживает набор аргументов, чем hello `Server`, так как он не прослушивателя автономный или может toobe, внедренный в это существующая платформа прослушивателя HTTP. Доступны также меньше возможностей с момента hello WebSocket управления является главным образом делегированного toohello служба ретрансляции.

Аргументы конструктора:

- `server`(обязательно) — hello полным URI для имя гибридного подключения на какие toolisten обычно создается с hello WebSocket.createRelayListenUri() вспомогательный метод.
- `token`(обязательно) — этот аргумент содержит строку ранее выданных маркеров или функции обратного вызова, который может быть вызван tooobtain маркера строки. параметр обратного вызова Hello предпочтителен, как позволяет обновления маркеров.

#### <a name="events"></a>События

`RelayedServer`экземпляры выдавать три события, которые включать вы toohandle входящие запросы, подключения и обнаружить условия ошибки. Необходимо подписаться toohello `connect` toohandle сообщения о событиях. 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

Hello `headers` событие возникает непосредственно перед принимается входящего подключения, включение изменения hello заголовки toosend toohello клиента. 

##### <a name="connection"></a>connection;

```JavaScript
function(socket)
```

Генерируется, когда принимается новое подключение WebSocket. Hello объект имеет тип `ws.WebSocket`, совпадает с базовым пакетом hello.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Если основной сервер hello выдает ошибку, он перенаправляется здесь.  

#### <a name="helpers"></a>Вспомогательные методы

Запуск toosimplify ретранслироваться сервера и немедленно подписка подключений tooincoming hello пакет предоставляет простой вспомогательную функцию, который также используется в примерах hello следующим образом:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Этот метод вызывает конструктор toocreate hello новый экземпляр hello RelayedServer и затем подписывается на событие toohello «подключения» указано hello обратного вызова.
 
##### <a name="relayedconnect"></a>relayedConnect

Просто зеркального отображения hello `createRelayedServer` вспомогательные функции, `relayedConnect` создает подключение клиента и подписывается на событие «открыто» toohello полученный сокете hello.

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

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о ретрансляции Azure в следующих статьях:
* [Что такое ретранслятор Azure?](relay-what-is-it.md)
* [Available Relay APIs](relay-api-overview.md) (Доступные API-интерфейсы ретранслятора)
