---
title: "aaaDebug микрослужбами Azure в Linux | Документы Microsoft"
description: "Узнайте, как toomonitor и диагностики вашей службы, написанные с помощью Microsoft Azure Service Fabric на локальном компьютере разработчика."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Мониторинг и диагностика состояния служб в локальной среде разработки


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Мониторинг, обнаружение, диагностика и устранение неполадок позволяют toocontinue служб с минимальными нарушениями toohello пользователями. Мониторинг и диагностика критически важны в фактически развернутой рабочей среде. Внедрение аналогичной модели во время разработки служб гарантирует, что диагностики конвейера hello работает при перемещении tooa рабочей среде. Service Fabric упрощает диагностику tooimplement разработчики службы, можно легко работайте с одним компьютером локальная разработка настройки и настройки кластера реальных рабочих.


## <a name="debugging-service-fabric-java-applications"></a>Отладка приложений Java в Service Fabric

Для приложений Java доступно [несколько платформ ведения журналов](http://en.wikipedia.org/wiki/Java_logging_framework) . Поскольку `java.util.logging` является параметром по умолчанию hello с hello JRE также используется для hello [примеров кода в github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hello следующее обсуждение объясняется, как tooconfigure hello `java.util.logging` framework.

С помощью java.util.logging, вы можете перенаправлять приложения журналы toomemory, выходных потоков, файлов консоли или сокетов. Для каждого из этих параметров существуют обработчики по умолчанию уже содержится в hello framework. Можно создать `app.properties` обработчика файлов tooconfigure hello файла для вашего приложения tooredirect все журналы tooa локального файла.

Следующий фрагмент кода Hello содержит пример конфигурации:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

hello указывает tooby папку Hello `app.properties` файл должен существовать. После hello `app.properties` создается файл, вы должны tooalso изменить сценарий точки входа, `entrypoint.sh` в hello `<applicationfolder>/<servicePkg>/Code/` свойство hello папки tooset `java.util.logging.config.file` слишком`app.propertes` файла. запись Hello должно иметь вид hello, следующий фрагмент кода:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


В результате применения этой конфигурации журналы будут циклически собираться в папку `/tmp/servicefabric/logs/`. файл журнала Hello в этом случае называется mysfapp%u.%g.log где:
* **%u** — уникальный номер tooresolve конфликтов между параллельных процессов Java.
* **%g** — toodistinguish номер поколения hello между поворот журналы.

По умолчанию, если обработчик не настроена явным образом, регистрируется обработчик консоли hello. Просмотреть журналы hello в системном журнале в разделе /var/log/syslog.

Дополнительные сведения см. в разделе hello [примеров кода в github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Отладка приложений C# в Service Fabric


Для трассировки приложений CoreCLR на платформе Linux доступно несколько платформ. Дополнительные сведения см. в разделе о [ведении журналов](http:/github.com/aspnet/logging) на сайте GitHub.  Так как разработчики знакомы tooC # EventSource "в этой статье используется EventSource для трассировки CoreCLR выборок в Linux.

Hello первым делом tooinclude System.Diagnostics.Tracing, чтобы можно было написать вашей toomemory журналы, выходные потоки или файлы консоли.  Для ведения журнала с помощью EventSource, добавьте следующий проект tooyour project.json hello:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Можно использовать настраиваемые toolisten EventListener для события службы hello и затем соответствующим образом перенаправит их tootrace файлы. Hello следующий фрагмент кода показывает пример реализации ведения журналов с помощью EventSource и пользовательские EventListener:


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


Hello предыдущем фрагменте выводит файл tooa журналы hello в `/tmp/MyServiceLog.txt`. Это имя файла должно toobe соответствующим образом обновлены. В случае, если требуется, чтобы журналы tooconsole tooredirect hello, используйте следующий фрагмент кода в классе настраиваемого EventListener hello:

```csharp
public static TextWriter Out = Console.Out;
```

Здравствуйте, образцов [примеры C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) использовать EventSource и пользовательский файл tooa события toolog EventListener.



## <a name="next-steps"></a>Дальнейшие действия
Здравствуйте добавлены же код трассировки приложения tooyour также работает с hello диагностики приложения на кластере Azure. Извлечение этих статей, которые рассматриваются различные варианты hello hello средств и описаны как tooset их вверх.
* [Каким образом toocollect ведет журнал диагностики Azure](service-fabric-diagnostics-how-to-setup-lad.md)
