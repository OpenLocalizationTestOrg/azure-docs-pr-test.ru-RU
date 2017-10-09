---
title: "aaaDevelop и выполнения Azure работает локально | Документы Microsoft"
description: "Узнайте, как toocode и тестирования Azure функционирует на локальном компьютере до их выполнения в функции Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Как программировать и тестировать функции Azure в локальной среде

При hello [портал Azure] предоставляет полный набор средств для разработки и тестирования функции Azure, многие разработчики предпочитают процесс локальной разработки. Функции Azure позволяет легко toouse избранные кода редактора и toodevelop средства локальной разработки и тестирования функций на локальном компьютере. Функции могут вызывать события в Azure, а вы можете отлаживать функции C# и JavaScript на локальном компьютере. 

Если вы используете Visual Studio C# для разработки, Функции Azure также [интегрируются с Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Установка инструментов основные функции hello Azure

Основные инструменты Azure функции является локальной версии функции Azure hello среды выполнения, который можно запустить на локальном компьютере Windows. Это не эмулятор или симулятор. Он имеет hello одной среды выполнения, лежит в основе функций в Azure.

Hello [основные инструменты Azure функции] предоставляется в виде пакета npm. Сначала необходимо [установить NodeJS](https://docs.npmjs.com/getting-started/installing-node), в состав которого входит npm.  

>[!NOTE]
>В настоящее время пакет основные инструменты Azure функции hello можно установить только на компьютерах Windows. Это ограничение действует из-за tooa временное ограничение в узле функции hello.

[основные инструменты Azure функции] добавляет hello следующие псевдонимы команд:
* **func**
* **azfun**
* **azurefunctions**

Все эти псевдоним может использоваться вместо `func` показано в примерах hello в этом разделе.

## <a name="create-a-local-functions-project"></a>Создание локального проекта службы "Функции"

При выполнении локально, проект функции — каталог, имеющий hello файлы host.json и local.settings.json. Этот каталог является hello эквивалентные функции приложения в Azure. toolearn Дополнительные сведения о hello Azure функции структуру папок, в разделе hello [руководство для разработчиков Azure функции](functions-reference.md#folder-structure).

В командной строке выполните следующую команду hello.

```
func init MyFunctionProj
```

Hello вывода выглядит как следующий пример hello.

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt за пределы Создание репозитория Git, используйте параметр hello `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Файл с локальными параметрами

файл local.settings.json Hello хранит параметры приложения, строки подключения и параметры для средства основных функций Azure. Он имеет hello следующие структуры:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Настройка      | Описание                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Если задано слишком**true**, все значения шифруются с помощью ключа локального компьютера. Используется с командами `func settings`. Значение по умолчанию — **false**. |
| **Значения** | Коллекция параметров приложения, используемых при локальном выполнении. Добавьте объект toothis параметров приложения.  |
| **AzureWebJobsStorage** | Задает hello toohello строка подключения учетной записи хранения Azure, который используется средой выполнения Azure функции hello. Учетная запись хранения Hello поддерживает ваша функция триггеры. Параметр подключения к учетной записи хранения необходим для всех функций, кроме функций, активируемых протоколом HTTP.  |
| **AzureWebJobsDashboard** | Задает hello соединения строки toohello учетную запись хранилища Azure, используемых toostore журналов функций hello. Это необязательное значение становится журналы hello, доступным в портал hello.|
| **Host** | Параметры в этом разделе настраивать функции hello хост-процесса, когда выполняется локально. | 
| **LocalHttpPort** | Порт по умолчанию, используемые при запуске hello локальный узел функции hello наборы (`func host start` и `func run`). Hello `--port` параметр командной строки имеют приоритет над это значение. |
| **CORS** | Определяет источники hello, разрешенное для [ресурсов независимо от источника (CORS) для управления доступом](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Источники указываются в виде разделенного запятыми списка без пробелов. Здравствуйте, использование подстановочного знака (**\***) поддерживается, который разрешает запросы из любого источника. |
| **ConnectionStrings** | Содержит hello строки подключения базы данных для функций. Строки подключения в этом объекте добавляются toohello среды с типом поставщика hello **System.Data.SqlClient**.  | 

Большинство триггеры и привязки **подключения** свойство, которое сопоставляет toohello имя параметра приложения или переменной среды. Для каждого свойства подключения должен быть определен параметр в файле local.settings.json. 

Эти параметры также могут считываться в коде как переменные среды. В C# используйте [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) или [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). Для JavaScript используйте `process.env`. Параметры, указанные как переменную среды имеют приоритет над значениями в файле local.settings.json hello. 

Параметры в файле local.settings.json hello используются только средствами функции при выполнении локально. По умолчанию эти параметры не переносятся автоматически при опубликованных tooAzure hello проекта. Используйте hello `--publish-local-settings` переключения [при публикации](#publish) toomake убедиться, что эти параметры будут добавлены toohello функции приложения в Azure.

Если задано не допустимую строку соединения хранения для **AzureWebJobsStorage**, отображается сообщение об ошибке после hello:  

>Отсутствует значение AzureWebJobsStorage в local.settings.json. This is required for all triggers other than HTTP. Выполните команду "func azure functionary fetch-app-settings <functionAppName>" или укажите строку подключения в файле local.settings.json.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Настройка параметров приложения

tooset значение для строки подключения, необходимо выполнить одно из следующих hello:
* Введите строку подключения hello из [обозреватель хранилищ Azure](http://storageexplorer.com/).
* Используйте один из следующих команд hello.

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Обе команды требуется вы toofirst входа tooAzure.

## <a name="create-a-function"></a>Создание функции

toocreate функции запуска hello следующую команду:

```
func new
``` 
`func new`поддерживает следующие необязательные аргументы hello:

| Аргумент     | Описание                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | Hello шаблон программирования на языке, например C#, F # или JavaScript. |
| **`--template -t`** | Имя шаблона Hello. |
| **`--name -n`** | имя функции Hello. |

Например toocreate триггер JavaScript HTTP запуска:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate функции активации очереди, выполните:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Запуск функций в локальной среде

toorun проект функции выполнять функции сервера hello. Hello узла включает триггеры для всех функций в проекте hello:

```
func host start
```

`func host start`hello поддерживает следующие параметры:

| Параметр     | Описание                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Hello toolisten локальных портов на. Значение по умолчанию: 7071. |
| **`--debug <type>`** | Параметры Hello `VSCode` и `VS`. |
| **`--cors`** | Список разрешенных источников CORS, разделенный запятыми без пробелов. |
| **`--nodeDebugPort -n`** | порт Hello для отладчика toouse hello узла. Значение по умолчанию — значение из launch.json или 5858. |
| **`--debugLevel -d`** | уровень трассировки Hello консоли (Выкл., verbose, информация, предупреждение или ошибка). Значение по умолчанию — info.|
| **`--timeout -t`** | Hello hello функции узла запуск, истечение времени ожидания в секундах. Значение по умолчанию — 20 секунд.|
| **`--useHttps`** | Привязать toohttps://localhost: {port} вместо toohttp://localhost: {port}. По умолчанию этот параметр создает доверенный сертификат на компьютере.|
| **`--pause-on-error`** | Приостановка для дополнительных входных данных перед выходом из процесса hello. Это удобно при запуске основных инструментов службы "Функции Azure" из интегрированной среды разработки (IDE).|

При запуске узла функции hello, он выводит hello функции активации HTTP URL-адрес:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Отладка в VS Code или Visual Studio

tooattach отладчик, передайте hello `--debug` аргумент. toodebug функции JavaScript, используют кода Visual Studio. Для функций на C# используйте Visual Studio.

функции toodebug C# используют `--debug vs`. Кроме того, можно использовать [инструменты Visual Studio 2017 для Функций Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

toolaunch hello узла и Настройка отладки JavaScript, выполните:

```
func host start --debug vscode
```

Затем в коде Visual Studio в hello **отладки** представление, выберите **прикрепляются функции tooAzure**. Вы можете присоединить точки останова, просмотреть значения переменных и осуществить пошаговое выполнение кода.

![Отладка с помощью Visual Studio 2015](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Функции tooa передача проверки данных

Можно также вызвать функцию напрямую с помощью `func run <FunctionName>` и предоставить входные данные для функции hello. Эта команда является toorunning аналогичные функции с помощью hello **тест** hello портал Azure на вкладке. Эта команда запускает hello всей функции узла.

`func run`hello поддерживает следующие параметры:

| Параметр     | Описание                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Встроенное содержимое. |
| **`--debug -d`** | Присоедините отладчик toohello хост-процесса перед выполнением функции hello.|
| **`--timeout -t`** | Toowait время (в секундах) до локальный узел функции hello готов.|
| **`--file -f`** | Здравствуйте toouse имя файла, как содержимое.|
| **`--no-interactive`** | Не запрашивает тип входных данных. Полезно для сценариев автоматизации.|

Например toocall функции активации HTTP и основной текст прохода, запустите следующую команду hello:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Публикация tooAzure

toopublish приложении функция tooa функции проекта в Azure, используйте hello `publish` команды:

```
func azure functionapp publish <FunctionAppName>
```

Можно использовать следующие варианты hello.

| Параметр     | Описание                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Параметры публикации в tooAzure local.settings.json, вывод запроса toooverwrite hello задание уже существует.|
| **`--overwrite-settings -y`** | Должен использоваться с `-i`. При другом значении перезаписывает локальное значение AppSettings в Azure. Значение по умолчанию — запрос.|

Hello `publish` команда отправляет содержимое hello каталог проекта функции hello. При удалении файлов в локальной системе hello `publish` команда не удаляет их из Azure. Можно удалить файлы в Azure с помощью hello [средство Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) в hello [портал Azure].

## <a name="next-steps"></a>Дальнейшие действия

Основные инструменты службы "Функции Azure" [имеют открытый код и размещаются на GitHub](https://github.com/azure/azure-functions-cli).  
запрос ошибку или компонент toofile [откройте вопрос GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[основные инструменты Azure функции]: https://www.npmjs.com/package/azure-functions-core-tools
[портал Azure]: https://portal.azure.com 
