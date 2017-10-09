
<span data-ttu-id="8dce2-101">Hello кода для всех функций hello в приложении для данной функции находится в корневой папке, содержащей файл конфигурации главного узла и один или несколько вложенных папок, содержащих код hello отдельную функцию, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="8dce2-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="8dce2-102">Hello *host.json* файл содержит некоторые конфигурации среды выполнения и располагается в корневой папке hello hello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="8dce2-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="8dce2-103">Сведения о доступных параметров см. в разделе [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) на вики-сайте репозитория WebJobs.Script hello.</span><span class="sxs-lookup"><span data-stu-id="8dce2-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="8dce2-104">Каждая функция имеет папку, содержащую один или несколько файлов кода, конфигурации function.json hello и другие зависимости.</span><span class="sxs-lookup"><span data-stu-id="8dce2-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

