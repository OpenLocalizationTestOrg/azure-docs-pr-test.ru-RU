---
title: "aaaGuidance для разработки функций Azure | Документы Microsoft"
description: "Узнайте hello Azure функции принципы и методы, необходимые функции toodevelop в Azure, для всех языков программирования и привязки."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "руководство разработчика, Функции Azure, функции, обработка событий, объекты webhook, динамические вычисления, независимая архитектура"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Руководство для разработчиков по Функциям Azure
В функции Azure определенные функции используют несколько основные технические концепции и компоненты, независимо от языка hello или привязки, которую вы используете. Прежде чем перейти к обучения сведения о конкретных tooa заданный язык или привязки, быть убедиться, что tooread через этот обзор, применяющий tooall из них.

В этой статье предполагается, что вы прочитали hello [обзор функции Azure](functions-overview.md) и не знакомы с [понятий SDK веб-заданий, таких как триггеры, привязки и среды выполнения JobHost hello](../app-service-web/websites-dotnet-webjobs-sdk.md). Функции Azure основан на hello SDK веб-заданий. 

## <a name="function-code"></a>Код функции
Объект *функция* является основной концепцией Azure функции hello. Написать код для функции на языке и сохранить hello и Здравствуйте, файлы конфигурации в одной папке. Конфигурация Hello называется `function.json`, который содержит данные конфигурации JSON. Различные языки поддерживаются, и у каждого toowork немного отличается взаимодействие с оптимизированными наилучшим образом подходит для этого языка. 

файл function.json Hello определяет привязки функций hello и других параметров конфигурации. Hello среды выполнения использует этот файл toodetermine hello события toomonitor и функционировать как toopass и возврат данных из выполнения. Hello ниже приведен пример файла function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Набор hello `disabled` свойство слишком`true` функции hello tooprevent выполнение.

Hello `bindings` свойство доступно, где настроить триггеров и привязки. Каждая привязка использует несколько общих параметров и некоторые параметры, которые являются определенной tooa определенного типа привязки. Каждая привязка требует hello следующие параметры:

| Свойство | Значения и типы | Комментарии |
| --- | --- | --- |
| `type` |string |Тип привязки. Пример: `queueTrigger`. |
| `direction` |"in", "out" |Указывает, является ли hello привязки для получения данных в функции hello или отправка данных из функции hello. |
| `name` |string |Hello имя, используемое для hello связанных данных в функции hello. Для C# это имя аргумента; код JavaScript он, ключ hello в список ключей и значений. |

## <a name="function-app"></a>Приложение-функция
Приложение-функция состоит из одной или нескольких независимых функций, совместно управляемых службой приложений Azure. Все функции hello в общей функции приложения hello же ценовой план, непрерывного развертывания и версии среды выполнения. Функции, написаны в нескольких языках могут все используют hello же функций приложения. Функции приложения в качестве tooorganize способ можно рассматривать и совместно управлять функций. 

## <a name="runtime-script-host-and-web-host"></a>Среда выполнения (средство обработки сценариев и веб-узел)
Среда Hello, или сервер сценариев — hello базовый пакет SDK веб-заданий узел, который прослушивает события, собирает и отправляет данные и выполняет код в конечном счете. 

триггеры toofacilitate HTTP, можно на веб-узел, разработанной toosit перед сервера сценариев hello в рабочих сценариях. Наличие двух узлов помогает tooisolate сервера сценариев hello hello обслуживающего трафика управляется hello веб-узел.

## <a name="folder-structure"></a>Структура папок
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Когда настройка проекта для развертывания функций tooa функции приложения в службе приложений Azure, можно обрабатывать следующую структуру папок, как код сайта. Для установки пакетов или транспиляции кода во время развертывания можно использовать существующие средства, такие как непрерывная интеграция и развертывание, или пользовательские сценарии развертывания.

> [!NOTE]
> Убедитесь, что toodeploy вашей `host.json` папки файла и функция непосредственно toohello `wwwroot` папки. Не включайте hello `wwwroot` папки в развертываниях. В противном случае вы получите папки `wwwroot\wwwroot`. 
> 
> 

## <a id="fileupdate"></a>Как tooupdate функции приложения файлы
Редактор функций Hello, встроенные в hello портал Azure позволяет обновлять hello *function.json* файл и файл кода hello для функции. tooupload или обновление других файлов, таких как *package.json* или *project.json* или зависимости, у вас toouse другие способы развертывания.

Функция приложений встроены в службе приложений и все hello [toostandard доступных веб-приложений, параметры развертывания](../app-service-web/web-sites-deploy.md) также доступны для приложений-функций. Ниже приведены некоторые методы можно использовать tooupload или обновить файлы функции приложения. 

#### <a name="toouse-app-service-editor"></a>toouse редактор службы приложения
1. На портале Azure функции hello щелкните **функции параметров приложения**.
2. В hello **Дополнительные параметры** щелкните **перейти параметры службы tooApp**.
3. Щелкните **Редактор службы приложений** на панели навигации меню приложения в разделе **Средства разработки**.
4. Щелкните **Переход**.
   
   После загрузки приложения службы редактора, вы увидите hello *host.json* файл и функция папках *wwwroot*. 
5. Tooedit открытых файлов, или путем перетаскивания из файлов tooupload компьютера разработки.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>приложение для toouse hello функция конечную точку SCM (Kudu)
1. Перейдите на страницу `https://<function_app_name>.scm.azurewebsites.net`.
2. Щелкните **Консоль отладки > CMD**.
3. Перейдите в слишком`D:\home\site\wwwroot\` tooupdate *host.json* или `D:\home\site\wwwroot\<function_name>` tooupdate функции и файлы.
4. Перетащите файла будет tooupload в соответствующей папке hello в сетке файл hello. Есть два элемента в сетке файл hello размещения файла. Для *.zip* файлы, появляется окно с меткой hello» Перетащите сюда tooupload и распакуйте.» Для других типов файлов удалите в сетке hello файла, но за пределами поля «Распакуйте» hello.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>toouse непрерывного развертывания
Следуйте инструкциям hello в разделе hello [непрерывного развертывания для функций Azure](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Параллельное выполнение
При нескольких активации события происходят быстрее, чем их можно обработать однопоточных функции среды выполнения, среда выполнения hello может вызывать функции hello несколько раз в параллельном режиме.  Если в приложении функции используется hello [потребления план размещения](functions-scale.md#how-the-consumption-plan-works), приложение hello функция удалось масштабируется автоматически.  Каждого экземпляра приложения функции hello, ли запускается приложение hello hello потребления размещение плана или обычной [план размещения службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), могут обрабатывать вызовы функций параллельных параллельно, используя несколько потоков.  Максимальное число одновременных функция вызовы в каждый экземпляр приложения функции Hello различается в зависимости от типа hello триггера, а также использовать другие функции в приложении функции hello ресурсы hello используется.

## <a name="functions-runtime-versioning"></a>Управление версиями среды выполнения Функций

Можно настроить hello версию функции среды hello hello `FUNCTIONS_EXTENSION_VERSION` параметра приложения. Например значение hello «~ 1» показывает, что функция приложения будут использовать 1 как его основной номер версии. Функция приложения — обновленных tooeach новый дополнительный номер версии, они будут выпущены. Можно просмотреть hello точную версию функции приложения hello **параметры** hello портале Azure на вкладке.

## <a name="repositories"></a>Репозитории
Hello кода для функций Azure открытым исходным кодом, который сохраняется в репозитории GitHub:

* [среда выполнения функций Azure;](https://github.com/Azure/azure-webjobs-sdk-script/)
* [портал функций Azure;](https://github.com/projectkudu/AzureFunctionsPortal)
* [шаблоны функций Azure;](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [пакет Azure SDK для веб-заданий;](https://github.com/Azure/azure-webjobs-sdk/)
* [расширения пакета Azure SDK для веб-заданий.](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Привязки
В таблице ниже приведены все поддерживаемые привязки.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Создание отчетов о проблемах
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Best Practices for Azure Functions](functions-best-practices.md) (Рекомендации по Функциям Azure)
* [Справочник разработчика C# по функциям Azure](functions-reference-csharp.md)
* [Справочник разработчика F# по функциям Azure](functions-reference-fsharp.md)
* [Справочник разработчика NodeJS по функциям Azure](functions-reference-node.md)
* [Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)](functions-triggers-bindings.md)
* [Функции Azure: hello пути](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) блоге группы разработчиков hello службе приложений Azure. В этой статье рассказывается история создания функций Azure.

