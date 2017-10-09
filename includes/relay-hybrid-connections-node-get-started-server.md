### <a name="create-a-nodejs-application"></a>Создание приложения Node.js

Создайте новый файл JavaScript с именем `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Добавление пакета NPM ретрансляции hello

Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.

### <a name="write-some-code-tooreceive-messages"></a>Написать код tooreceive сообщений

1. Добавьте следующие константы toohello вверху hello hello `listener.js` файла.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Добавьте следующие константы toohello hello `listener.js` hello гибридного подключения сведения в файле. Замените заполнители hello в квадратных скобках со значениями hello, полученными при создании hello гибридного подключения.
   
   1. `const ns`-hello ретрансляции пространства имен. Быть полным именем пространства имен, что toouse hello; например `{namespace}.servicebus.windows.net`.
   2. `const path`-Имя hello hello гибридного подключения.
   3. `const keyrule`-hello имя ключа SAS hello.
   4. `const key`-hello значение ключа SAS.

3. Добавьте следующий код toohello hello `listener.js` файла:
   
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

