---
title: "рекомендации aaaBest и руководстве по устранению неполадок для узла приложений на веб-приложениях Azure"
description: "Сведения, рекомендации по обеспечению hello и действия по устранению неполадок для узла приложений на веб-приложения Azure."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Рекомендации и руководство по устранению неполадок приложений Node в веб-приложениях Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

В этой статье вы узнаете hello рекомендации и действия по устранению неполадок [узла приложения](app-service-web-get-started-nodejs.md) на веб-приложений Azure (с [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Будьте осторожны при выполнении действий по устранению неполадок на рабочем сайте. Рекомендуется tootroubleshoot приложения в рабочей установки, например вашей промежуточный слот и после устранения проблемы hello буферов в промежуточный слот на производственный слот.
> 
> 

## <a name="iisnode-configuration"></a>Конфигурация IISNODE
Это [файл схемы](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) показывает все параметры hello, которые могут быть настроены для iisnode. Ниже приведены некоторые параметры hello, которые будут использоваться для приложения.

* nodeProcessCountPerApplication
  
    Этот параметр управляет числом hello узел процессов, запускаемых на каждое приложение IIS. Значение по умолчанию — 1. Установив этот too0 можно запустить столько node.exe как число ядер вашей виртуальной Машины. Рекомендуемое значение — 0 для большинства приложений, поэтому можно использовать все hello ядер на компьютере. Node.exe выполняется в одном потоке, поэтому один node.exe будет занимать более 1 ядра и tooget максимальной производительности узла приложения, необходимо tooutilize все ядра.
* nodeProcessCommandLine
  
    Этот параметр управляет node.exe toohello путь hello. Можно задать это значение toopoint tooyour node.exe версии.
* maxConcurrentRequestsPerProcess
  
    Этот параметр определяет максимальное количество одновременных запросов, отправленных iisnode tooeach node.exe hello. На веб-приложения azure значение по умолчанию hello равно Infinite. Tooworry об этом параметре не будет. За пределами azure веб-приложений hello значение по умолчанию — 1024. Вы можете tooconfigure, получает это в зависимости от того, сколько запросов приложения и как быстро приложение обрабатывает каждый запрос.
* maxNamedPipeConnectionRetry
  
    Этот параметр управляет hello максимальное число iisnode повторит попытку внесения подключение с именем канала toosend hello запрос через toonode.exe hello. Этот параметр в сочетании с namedPipeConnectionRetryDelay определяет hello общее время ожидания в пределах iisnode каждого запроса. В веб-приложениях Azure для этого параметра по умолчанию задано значение 200. Общее время ожидания в секундах равно произведению maxNamedPipeConnectionRetry \*на namedPipeConnectionRetryDelay, разделенному на 1000.
* namedPipeConnectionRetryDelay
  
    Этот параметр элементы управления hello объем iisnode время (в мс) будет ожидать между каждой toosend для повтора запроса toonode.exe через именованный канал hello. Значение по умолчанию — 250 мс.
    Общее время ожидания в секундах равно произведению maxNamedPipeConnectionRetry \*на namedPipeConnectionRetryDelay, разделенному на 1000.
  
    По умолчанию hello общее время ожидания в iisnode на веб-приложений azure — 200 \* 250 секунд = 50 секунд.
* logDirectory
  
    Этот параметр управляет hello каталог, где iisnode регистрируют stdout и stderr. Значение по умолчанию — iisnode, который является относительным toohello основной скрипт directory (каталог, где присутствует основной server.js)
* debuggerExtensionDll
  
    Этот параметр определяет версию средства node-inspector, которую iisnode будет использовать при выполнении отладки приложения Node. В настоящее время iisnode инспектора 0.7.3.dll и iisnode inspector.dll являются допустимыми значениями этого параметра hello только 2. По умолчанию для этого параметра задано значение iisnode-inspector-0.7.3.dll. версия iisnode инспектора 0.7.3.dll использует узел инспектора 0.7.3 и использует websockets, поэтому вам необходимо будет tooenable websockets на ваш toouse azure веб-приложение этой версии. В разделе <http://www.ranjithr.com/?p=98> Дополнительные сведения о как tooconfigure iisnode toouse hello новый узел Инспектор.
* flushResponse
  
    поведение по умолчанию Hello служб IIS, что он помещает в буфер данные ответа вверх too4MB перед сбросом, или до конца hello hello ответа, что наступит раньше. iisnode предлагает параметр toooverride такое поведение конфигурации: tooflush фрагмент текст сущности ответа hello как можно скорее iisnode получит его из node.exe, вы должны tooset hello iisnode/@flushResponse атрибута в web.config too'true ":
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Очистка каждого фрагмента текст сущности ответа hello задействуется снижение производительности, снижает пропускную способность hello hello системы на ~ 5% (по состоянию на v0.1.13), поэтому этот параметр только tooendpoints, требующие ответа потоковой передачи (например, при использовании hello наилучшим образом tooscope <location> элемента в файле web.config hello)
  
    В toothis сложения для потоковой передачи приложений, необходимо будет tooalso responseBufferLimit набор из вашего too0 iisnode обработчика.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Это список разделенных точкой с запятой файлов, в которых будут отслеживаться изменения. Изменение файла tooa вызывает toorecycle приложения hello. Каждая запись состоит из имени необязательно каталога, а также имя требуемого файла, которое toohello относительный каталог, где находится точка входа для основного приложения hello. В части имени файла hello только допускаются подстановочные знаки. Значение по умолчанию — \*.js;web.config.
* recycleSignalEnabled
  
    Значение по умолчанию — false. Если параметр включен, приложение узел сможет подключиться tooa именованного канала (переменная среды IISNODE\_УПРАВЛЕНИЯ\_КАНАЛА) и отправить сообщение «Корзина». Это приведет к hello w3wp toorecycle надлежащим образом.
* idlePageOutTimePeriod
  
    По умолчанию для этого параметра используется значение 0, а это значит, что он отключен. При toosome установите значение больше 0, iisnode будет откачивать страницы из его дочерних процессов каждые «idlePageOutTimePeriod» миллисекунд. toounderstand откачивать означает, что страницы можно найти toothis [документации](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Этот параметр будет использоваться для приложений, потребляющих большой объем памяти и хотите toodisk памяти toopageout иногда toofree некоторые оперативной памяти.

> [!WARNING]
> Соблюдайте осторожность при включении hello Далее параметры конфигурации приложений в производственной среде. Рекомендуется toonot Включение динамической производственных приложений.
> 
> 

* debugHeaderEnabled
  
    значение по умолчанию Hello имеет значение false. Если задать tootrue, iisnode добавит ответ заголовок отладки iisnode tooevery HTTP ответа HTTP отправляет значение заголовка hello iisnode отладки является URL-адрес. Отдельные части диагностических сведений можно достигнутой, просмотрев hello фрагмент URL-адреса, но гораздо Улучшенная визуализация достигается открытием hello URL-адрес в браузере hello.
* loggingEnabled
  
    Этот параметр управляет ведения журнала hello stdout и stderr, iisnode. Iisnode будет stdout и stderr из узла процессов, которые он запускает захвата и записи toohello каталог, указанный в параметре «logDirectory» hello. После включения приложения будет записывать журналы toohello файловой системы, в зависимости от объема hello ведения журнала, выполненную приложения hello, возможно влияние на производительность.
* devErrorsEnabled
  
    Значение по умолчанию — false. Если значение tootrue, iisnode отображает код состояния hello HTTP и код ошибки Win32 в браузере. Код win32 Hello будут полезными при отладке определенных типов проблем.
* debuggingEnabled (не включайте этот параметр на активном рабочем сайте)
  
    Этот параметр определяет функцию отладки. В iisnode интегрировано средство node-inspector. Включение этого параметра активирует отладку приложения Node. После включения этого параметра iisnode будет файлы необходимости узел инспектора hello макета в каталоге «debuggerVirtualDir» на hello первого отладки запроса tooyour узла приложения. Можно загрузить hello узел инспектора, отправляя toohttp://yoursite/server.js/debug запроса. Сегмент URL-адреса hello отладки можно управлять с параметром «debuggerPathSegment». По умолчанию для этого параметра используется значение debug. Можно задать этот tooa GUID, например, чтобы оно было труднее toobe обнаруженные другими пользователями.
  
    Дополнительные сведения об отладке см. [здесь](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html).

## <a name="scenarios-and-recommendationstroubleshooting"></a>Сценарии, рекомендации и устранение неполадок
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>В этом сценарии приложение Node отравляет слишком много вызовов.
Во многих приложениях необходимо toomake исходящие подключения как часть их нормальной работе. Например при поступлении запроса приложения узла будет требуется toocontact REST API в другом месте-запрос hello tooprocess некоторые сведения. При выполнении вызовов http или https, необходимо toouse keep alive агента. Например можно использовать модуль agentkeepalive hello агентом keep alive при выполнении этих исходящих вызовов. Это гарантирует повторного hello сокетов на вашей виртуальной Машины azure веб-приложения и уменьшая hello сократить затраты на создание новых сокетов для каждого исходящего запроса. Кроме того это гарантирует, что вы используете число меньше toomake сокеты много исходящих запросов и поэтому не должно превышать значение параметра maxSockets hello, который выделяется на виртуальную Машину. Рекомендации по веб-приложения Azure была бы значение параметра maxSockets agentKeepAlive hello tooset значение tooa всего 160 сокетов каждой виртуальной Машины. Это означает, что при наличии 4 node.exe на hello виртуальной Машины нужно tooset hello agentKeepAlive значение параметра maxSockets too40 за node.exe которой равно 160 общее каждой виртуальной Машины.

Пример конфигурации модуля [agentKeepALive](https://www.npmjs.com/package/agentkeepalive):

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

В этом примере предполагается, что на виртуальной машине запущено 4 файла node.exe. При наличии Разное количество node.exe на hello ВМ будет иметь параметр соответственно значение параметра maxSockets hello toomodify.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Чрезмерное потребление ресурсов ЦП приложением Node
На вашем портале может отобразиться оповещение от веб-приложений Azure о высоком потреблении ресурсов ЦП. Вы также можете toowatch мониторов настройки для определенных [метрики](web-sites-monitor.md). При проверке использование hello ЦП на hello [панели мониторинга портала Azure](../application-insights/app-insights-web-monitor-performance.md), проверьте hello МАКСИМАЛЬНЫЕ значения для ЦП, не пропустите Здравствуй пиковыми значениями.
В случаях, когда вы считаете приложение потребляет слишком много ЦП, и вы не можете объяснить, почему это происходит необходимо будет tooprofile узла приложения.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Профилирование приложения Node в веб-приложениях Azure с помощью средства V8-Profiler
Позволяет, например, предположим, что приложение hello world, что требуется tooprofile, как показано ниже:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Перейдите на сайт https://yoursite.scm.azurewebsites.net/DebugConsole tooyour scm

Откроется следующая командная строка. Перейдите в каталог site/wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Выполните команду hello, «npm install v8 профилировщик»

В каталоге node\_modules установится средство v8-profiler и все его зависимости.
Теперь измените вашей tooprofile server.js приложения.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Hello выше изменения будет профилировать WriteConsoleLog функции hello, а затем написать too'profile.cpuprofile выходные данные профиля hello "файл в папке wwwroot вашего сайта. Отправьте запрос tooyour приложения. В каталоге site wwwroot будет создан файл profile.cpuprofile.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Загрузить этот файл и необходимо будет tooopen этого файла в хром кнопкой F12. Нажмите клавишу F12 в chrome, затем нажмите «Вкладка «Профили»» hello. Нажмите кнопку "Загрузить". Выберите только что загруженный файл profile.cpuprofile. Щелкните только что загружен профиль hello.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Вы увидите, что 95% времени hello затраченного на WriteConsoleLog функции, как показано ниже. Это также показывает номера hello точных строк и исходных файлов, вызывающие проблемы hello.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Чрезмерное потребление памяти приложением Node
На вашем портале может отобразиться оповещение от веб-приложений Azure о высоком потреблении памяти. Вы также можете toowatch мониторов настройки для определенных [метрики](web-sites-monitor.md). При проверке hello использование памяти на hello [панели мониторинга портала Azure](../application-insights/app-insights-web-monitor-performance.md), проверьте hello МАКСИМАЛЬНОЕ значения для памяти, не пропустите Здравствуй пиковыми значениями.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Обнаружение утечки и определение различий кучи для node.js
Можно использовать [memwatch узел](https://github.com/lloyd/node-memwatch) утечек toohelp идентификации памяти.
Можно установить memwatch так же, как профилировщик v8 и редактирования, которую ваш код diff и toocapture куч tooidentify hello утечки памяти в приложении.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Случайное завершение работы файла node.exe
Это может произойти по нескольким причинам.

1. Приложение создает неперехваченных исключений — d: выполните проверку\\домашней\\LogFiles\\приложения\\errors.txt ведения журнала сведения в файле hello на hello возникло исключение. Этот файл имеет hello трассировки стека, поэтому вы можете исправить исходя из этого приложения.
2. Приложение потребляет слишком много памяти, что изначально влияет на другие процессы. Если закрыть too100% hello общий объем памяти виртуальной Машины, ваш node.exe удалось завершен по toolet manager hello процесс другие процессы получить toodo вероятность некоторую работу. toofix это, убедитесь, что приложение не может вызывать утечку памяти или если после этого приложение действительно должен toouse большой объем памяти, можно масштабировать tooa большего размера виртуальной Машины с гораздо больше оперативной памяти.

### <a name="my-node-application-does-not-start"></a>Ошибка запуска приложения Node
Если при запуске приложения возвращаются ошибки с кодом 500, причин может быть несколько.

1. Node.exe отсутствует правильное расположение hello. Проверьте параметр nodeProcessCommandLine.
2. Основной скрипт файл отсутствует правильное расположение hello. Web.config и убедитесь, что имя hello hello основной скрипт файла в основной скрипт hello обработчики раздела соответствует hello файл.
3. Используется неправильная конфигурация Web.config: Проверьте имена и значения параметров hello.
4. Холодный запуск – приложения занимает слишком много времени toostartup. Если для запуска приложения требуется больше времени, чем задано для общего времени ожидания в секундах ((maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay), разделенное на 1000), iisnode вернет ошибку с кодом 500. Увеличьте значения этих toomatch параметры приложения запустите iisnode tooprevent время из превышения времени ожидания и возвращая ошибку hello 500 hello.

### <a name="my-node-application-crashed"></a>Сбой приложения Node
Приложение создает неперехваченных исключений — d: выполните проверку\\домашней\\LogFiles\\приложения\\errors.txt ведения журнала сведения в файле hello на hello возникло исключение. Этот файл имеет hello трассировки стека, поэтому вы можете исправить исходя из этого приложения.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Узел приложения занимает слишком много времени, toostartup (холодный запуск)
Наиболее распространенной причиной этого является, приложение hello имеет большое количество файлов в узле hello\_модули и tooload попытками приложения hello большинство этих файлов во время запуска. По умолчанию так как файлы расположены в сетевой папке hello на веб-приложения Azure, загрузка такого большого количества файлов может занять некоторое время.
Некоторые решения toomake это быстрее являются:

1. Убедитесь, что у вас есть структура плоский зависимостей и зависимости, не повторяющиеся с помощью npm3 tooinstall модулей.
2. Повторите toolazy нагрузки на узле\_модулей и не загружать все модули hello во время запуска. Это означает, что вызов этого hello toorequire('module') должно осуществляться при действительно нужны внутри функции hello повторите toouse hello модуля.
3. В веб-приложениях Azure используется функция, которая называется "локальный кэш". Эта функция копирует содержимое из hello сетевой общей папки toohello локальный диск на hello виртуальной Машины. Здравствуйте, так как файлы hello являются локальными, время узла загрузки\_модулей выполняется гораздо быстрее. -Этот [документации](../app-service/app-service-local-cache.md) объясняет, как toouse локальный кэш в более подробно.

## <a name="iisnode-http-status-and-substatus"></a>Состояние и подсостояние HTTP обработчика iisnode
Это [исходный файл](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) списки, могут возвращать все iisnode комбинации возможные состояния/подсостояния hello в случае ошибки.

Включить FREB для кода ошибки win32 приложения toosee hello (Убедитесь, что включен FREB только на узлах нерабочей по соображениям производительности).

| Состояние HTTP | Подсостояние HTTP | Возможная причина |
| --- | --- | --- |
| 500 |1000 |Некоторые проблемы, диспетчеризации tooIISNODE hello запрос — проверьте, если node.exe была запущена. Возможно, при запуске этого файла произошел сбой. Проверьте конфигурацию web.config на наличие ошибок. |
| 500 |1001 |-URL-адрес toohello Win32Error 0x2 — приложение не отвечает. URL-адрес проверки перепишите правила или если приложение express имеет hello правильный маршрутов, указанных. -Win32Error 0x6d — именованный канал занят: Node.exe не принимает запросы из-за занятости hello канала. Проверьте потребление ресурсов ЦП. Другие ошибки. Проверьте файл node.exe на наличие повреждений. |
| 500 |1002 |Файл node.exe поврежден. Для трассировки стека проверьте файл d:\\home\\LogFiles\\logging-errors.txt. |
| 500 |1003 |Конфигурации канала проблема — вы никогда не увидите это, но неверное случае hello с именем конфигурации канала. |
| 500 |1004–1018 |Возникла какая-либо ошибка при отправке hello запроса или обработки ответа hello из node.exe. Проверьте файл node.exe на наличие повреждений. Для трассировки стека проверьте файл d:\\home\\LogFiles\\logging-errors.txt. |
| 503 |1000 |Не хватает памяти tooallocate более именованных каналов. Проверьте, почему приложение потребляет такое большое количество памяти. Проверьте значение параметра maxConcurrentRequestsPerProcess. Если он не бесконечно и вы с большим числом запросов, увеличить это значение tooprevent ошибки. |
| 503 |1001 |Запрос не может быть отправлено toonode.exe из-за перезапуска приложения hello. После после перезапуска приложения hello, запросы должны обслуживаться обычным образом. |
| 503 |1002 |Проверьте код ошибки win32 для фактическая причина — запрос не может быть отправлено tooa node.exe. |
| 503 |1003 |Именованный канал слишком занят. Проверьте, не потребляет ли узел слишком много ресурсов ЦП. |

В файле node.exe содержится параметр, который называется NODE\_PENDING\_PIPE\_INSTANCES. По умолчанию за пределами веб-приложения Azure для этого параметра задано значение 4. Это означает, что во время на hello именованного канала, node.exe может принимать только 4 запроса. На веб-приложения Azure это значение too5000, и это значение должно быть достаточно для большинства приложений узла на веб-приложения azure. Не должны видеть 503.1003 на веб-приложения azure, так как у нее высокое значение hello узел\_Ожидание\_КАНАЛА\_ЭКЗЕМПЛЯРОВ.  |

## <a name="more-resources"></a>Дополнительные ресурсы
Выполните эти дополнительные сведения о приложениях node.js toolearn ссылки на службу приложений Azure.

* [Приступая к работе с веб-приложениями Node.js в службе приложений Azure](app-service-web-get-started-nodejs.md)
* [Как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md)
* [Использование модулей Node.js с приложениями Azure](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps: Node.js (Веб-приложения службы приложений Azure: Node.js)](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Центр разработчиков Node.js.](../nodejs-use-node-modules-azure-apps.md)
* [Изучение hello консоли отладки Kudu Super секрет](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

