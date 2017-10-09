### <a name="create-a-nodejs-application"></a>Создание приложения Node.js

Создайте новый файл JavaScript с именем `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Добавление пакета NPM ретрансляции hello

Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.

### <a name="write-some-code-toosend-messages"></a>Написать код toosend сообщений

1. Добавьте следующее hello `constants` toohello вверху hello `sender.js` файла.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Добавьте следующие константы toohello hello `sender.js` hello гибридного подключения сведения в файле. Замените заполнители hello в квадратных скобках со значениями hello, полученными при создании hello гибридного подключения.
   
   1. `const ns`-hello ретрансляции пространства имен. Быть полным именем пространства имен, что toouse hello; например `{namespace}.servicebus.windows.net`.
   2. `const path`-Имя hello hello гибридного подключения.
   3. `const keyrule`-hello имя ключа SAS hello.
   4. `const key`-hello значение ключа SAS.

3. Добавьте следующий код toohello hello `sender.js` файла:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Файл sender.js должен выглядеть следующим образом:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

