### <a name="create-a-nodejs-application"></a>Создание приложения Node.js

Создайте новый файл JavaScript с именем `listener.js`.

### <a name="add-the-relay-npm-package"></a>Добавление пакета ретранслятора NPM

Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.

### <a name="write-some-code-to-receive-messages"></a>Написание кода для получения сообщений

1. Добавьте следующую константу в верхнюю часть файла `listener.js`.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Добавьте следующие константы в файл `listener.js` для сведений о гибридном подключении. Замените заполнители в скобках значениями, которые получены при создании гибридного подключения.
   
   1. `const ns` — пространство имен ретранслятора. Необходимо использовать полное имя пространства имен, например `{namespace}.servicebus.windows.net`.
   2. `const path` — имя гибридного подключения.
   3. `const keyrule` — имя ключа SAS.
   4. `const key` — значение ключа SAS.

3. Добавьте в файл `listener.js` следующий код:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Вот как будет выглядеть файл listener.js:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

