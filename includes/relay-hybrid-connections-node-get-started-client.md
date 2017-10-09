### <a name="create-a-nodejs-application"></a><span data-ttu-id="e70ab-101">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="e70ab-101">Create a Node.js application</span></span>

<span data-ttu-id="e70ab-102">Создайте новый файл JavaScript с именем `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="e70ab-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="e70ab-103">Добавление пакета NPM ретрансляции hello</span><span class="sxs-lookup"><span data-stu-id="e70ab-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="e70ab-104">Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="e70ab-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="e70ab-105">Написать код toosend сообщений</span><span class="sxs-lookup"><span data-stu-id="e70ab-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="e70ab-106">Добавьте следующее hello `constants` toohello вверху hello `sender.js` файла.</span><span class="sxs-lookup"><span data-stu-id="e70ab-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="e70ab-107">Добавьте следующие константы toohello hello `sender.js` hello гибридного подключения сведения в файле.</span><span class="sxs-lookup"><span data-stu-id="e70ab-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="e70ab-108">Замените заполнители hello в квадратных скобках со значениями hello, полученными при создании hello гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="e70ab-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="e70ab-109">`const ns`-hello ретрансляции пространства имен.</span><span class="sxs-lookup"><span data-stu-id="e70ab-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="e70ab-110">Быть полным именем пространства имен, что toouse hello; например `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e70ab-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="e70ab-111">`const path`-Имя hello hello гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="e70ab-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="e70ab-112">`const keyrule`-hello имя ключа SAS hello.</span><span class="sxs-lookup"><span data-stu-id="e70ab-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="e70ab-113">`const key`-hello значение ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="e70ab-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="e70ab-114">Добавьте следующий код toohello hello `sender.js` файла:</span><span class="sxs-lookup"><span data-stu-id="e70ab-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="e70ab-115">Файл sender.js должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e70ab-115">Here is what your sender.js file should look like:</span></span>
   
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

