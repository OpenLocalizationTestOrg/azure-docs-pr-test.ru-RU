---
title: "aaaDebug приложения структуры службы Azure в Eclipse | Документы Microsoft"
description: "Улучшить hello надежность и производительность служб по разработке и отладке их в Eclipse в кластере локальной разработки."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Отладка приложения Java Service Fabric с помощью Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio и CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse и Java](service-fabric-debugging-your-application-java.md)
> 

1. Запуск разработки локального кластера с помощью инструкции hello в [Настройка среды разработки Service Fabric](service-fabric-get-started-linux.md).

2. Обновить entryPoint.sh hello службы нужно toodebug, таким образом, процесс hello java с параметрами удаленной отладки. Этот файл можно найти в следующие расположения hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Для отладки в этом примере задается порт 8001.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Обновить манифест приложения hello, задав число экземпляров hello или hello счетчика реплики для hello службы, для которого создается отлаживать too1. Этот параметр позволяет избежать конфликтов для hello порт, который используется для отладки. Например, для служб без отслеживания состояния, задайте ``InstanceCount="1"`` и для служб с отслеживанием состояния набора hello целевого объекта и min набора реплик размеры too1 следующим образом: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Развертывание приложения hello.

5. В hello интегрированной среды разработки Eclipse, выберите **выполнения -> Отладка конфигурации -> удаленное приложение Java и входных свойств подключения** и задайте свойства hello следующим образом:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Установите точки останова в нужные моменты и отладить приложение hello.

Если произошло аварийное завершение приложения hello, можно также tooenable coredumps. Выполните ``ulimit -c`` в оболочке. Если возвращается 0, то функция coredumps не включена. tooenable неограниченное coredumps выполните следующую команду hello: ``ulimit -c unlimited``. Можно также проверить состояние hello, с помощью команды hello ``ulimit -a``.  Если требуется путь создания coredump hello tooupdate выполнение ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Дальнейшие действия

* [Сбор журналов с помощью системы диагностики Azure](service-fabric-diagnostics-how-to-setup-lad.md).
* [Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
