### <a name="create-a-nodejs-application"></a><span data-ttu-id="c04fe-101">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="c04fe-101">Create a Node.js application</span></span>

<span data-ttu-id="c04fe-102">Создайте новый файл JavaScript с именем `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="c04fe-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="c04fe-103">Добавление пакета NPM ретрансляции hello</span><span class="sxs-lookup"><span data-stu-id="c04fe-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="c04fe-104">Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="c04fe-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="c04fe-105">Написать код tooreceive сообщений</span><span class="sxs-lookup"><span data-stu-id="c04fe-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="c04fe-106">Добавьте следующие константы toohello вверху hello hello `listener.js` файла.</span><span class="sxs-lookup"><span data-stu-id="c04fe-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="c04fe-107">Добавьте следующие константы toohello hello `listener.js` hello гибридного подключения сведения в файле.</span><span class="sxs-lookup"><span data-stu-id="c04fe-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="c04fe-108">Замените заполнители hello в квадратных скобках со значениями hello, полученными при создании hello гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="c04fe-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="c04fe-109">`const ns`-hello ретрансляции пространства имен.</span><span class="sxs-lookup"><span data-stu-id="c04fe-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="c04fe-110">Быть полным именем пространства имен, что toouse hello; например `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c04fe-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="c04fe-111">`const path`-Имя hello hello гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="c04fe-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="c04fe-112">`const keyrule`-hello имя ключа SAS hello.</span><span class="sxs-lookup"><span data-stu-id="c04fe-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="c04fe-113">`const key`-hello значение ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="c04fe-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="c04fe-114">Добавьте следующий код toohello hello `listener.js` файла:</span><span class="sxs-lookup"><span data-stu-id="c04fe-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="c04fe-115">Вот как будет выглядеть файл listener.js:</span><span class="sxs-lookup"><span data-stu-id="c04fe-115">Here is what your listener.js file should look like:</span></span>
   
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

