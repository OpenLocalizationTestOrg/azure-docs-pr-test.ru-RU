
Hello кода для всех функций hello в приложении для данной функции находится в корневой папке, содержащей файл конфигурации главного узла и один или несколько вложенных папок, содержащих код hello отдельную функцию, как следующий пример hello:

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

Hello *host.json* файл содержит некоторые конфигурации среды выполнения и располагается в корневой папке hello hello функции приложения. Сведения о доступных параметров см. в разделе [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) на вики-сайте репозитория WebJobs.Script hello.

Каждая функция имеет папку, содержащую один или несколько файлов кода, конфигурации function.json hello и другие зависимости.

