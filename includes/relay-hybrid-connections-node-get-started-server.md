### <a name="create-a-nodejs-application"></a><span data-ttu-id="8a003-101">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="8a003-101">Create a Node.js application</span></span>

<span data-ttu-id="8a003-102">Создайте новый файл JavaScript с именем `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="8a003-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="8a003-103">Добавление пакета ретранслятора NPM</span><span class="sxs-lookup"><span data-stu-id="8a003-103">Add the Relay NPM package</span></span>

<span data-ttu-id="8a003-104">Запустите `npm install hyco-ws` из командной строки NPM в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="8a003-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-receive-messages"></a><span data-ttu-id="8a003-105">Написание кода для получения сообщений</span><span class="sxs-lookup"><span data-stu-id="8a003-105">Write some code to receive messages</span></span>

1. <span data-ttu-id="8a003-106">Добавьте следующую константу в верхнюю часть файла `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="8a003-106">Add the following constant to the top of the `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="8a003-107">Добавьте следующие константы в файл `listener.js` для сведений о гибридном подключении.</span><span class="sxs-lookup"><span data-stu-id="8a003-107">Add the following constants to the `listener.js` file for the hybrid connection details.</span></span> <span data-ttu-id="8a003-108">Замените заполнители в скобках значениями, которые получены при создании гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="8a003-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="8a003-109">`const ns` — пространство имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="8a003-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="8a003-110">Необходимо использовать полное имя пространства имен, например `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="8a003-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="8a003-111">`const path` — имя гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="8a003-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="8a003-112">`const keyrule` — имя ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="8a003-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="8a003-113">`const key` — значение ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="8a003-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="8a003-114">Добавьте в файл `listener.js` следующий код:</span><span class="sxs-lookup"><span data-stu-id="8a003-114">Add the following code to the `listener.js` file:</span></span>
   
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
    <span data-ttu-id="8a003-115">Вот как будет выглядеть файл listener.js:</span><span class="sxs-lookup"><span data-stu-id="8a003-115">Here is what your listener.js file should look like:</span></span>
   
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

