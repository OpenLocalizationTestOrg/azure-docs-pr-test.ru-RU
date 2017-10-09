---
title: "Статистическая обработка событий Service Fabric с диагностикой Azure Linux aaaAzure | Документы Microsoft"
description: "Ознакомьтесь со сведениями об агрегировании и сборе событий с использованием LAD для мониторинга и диагностики кластеров Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Агрегирование и сбор событий с помощью системы диагностики Azure для Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении. Наличие журналы hello в центральном расположении, помогает выполнить анализ и устранение проблем в кластере, или в hello приложений и служб, работающих в этом кластере.

Собирать журналы и tooupload один из способов — toouse hello диагностики Azure Linux (LAD) расширения, которое отправляет журналы tooAzure хранилища и имеет hello параметр toosend журналы tooAzure Application Insights или концентраторов событий. Можно также использовать внешний процесс tooread hello событий из хранилища и поместите их в платформа продуктом анализа [аналитики журнала OMS](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала.

## <a name="log-and-event-sources"></a>Источники журналов и событий

### <a name="service-fabric-platform-events"></a>События платформы Service Fabric
Service Fabric создает несколько готовых журналов посредством [LTTng](http://lttng.org), включая журналы операционных событий и событий среды выполнения. Эти журналы хранятся в расположении hello hello указывает шаблона диспетчера ресурсов кластера. tooget или набор учетных данных хранилища hello, найдите тег hello **AzureTableWinFabETWQueryable** и выполните поиск **StoreConnectionString**.

### <a name="application-events"></a>События приложения
 События, которые создаются кодом ваших приложений и служб согласно вашим указаниям во время инструментирования программного обеспечения. Вы можете использовать любое решение для ведения журналов, которое создает текстовые файлы журнала, например LTTng. Дополнительные сведения см. на трассировки приложения hello LTTng документации.

[Мониторинг и диагностика состояния служб в локальной среде разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

## <a name="deploy-hello-diagnostics-extension"></a>Развертывание расширения диагностики hello
Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello. Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами. Hello действия различаются в зависимости от hello портал Azure или диспетчера ресурсов Azure.

задать toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера **диагностики** слишком**на**. После создания кластера hello, этот параметр нельзя изменить с помощью портала hello.

Затем настройте файлы hello toocollect диагностики Azure Linux (LAD) и поместите их в вашей учетной записи хранилища. Этот процесс описан в сценарии 3 («отправить файлы журнала») в статье hello [toomonitor с помощью LAD и диагностики виртуальных машин Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). После этого возвращает процесс, вы доступ toohello трассировки. Можно передать hello визуализатора tooa трассировок по своему усмотрению.

Можно также развернуть hello расширения диагностики с помощью диспетчера ресурсов Azure. Hello процесс аналогичен для Windows и Linux и задокументирован для кластеров Windows в [как toocollect журналы с диагностикой Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Также можно использовать Operations Management Suite, как описано в статье [Анализ журналов Operations Management Suite в Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

После завершения этой конфигурации агента отслеживание hello LAD hello указанные файлы журнала. Всякий раз, когда строки присоединенных toohello файл, он создает запись системного журнала, отправленных toohello хранения, указанной.

## <a name="next-steps"></a>Дальнейшие действия

какие события следует изучить при диагностике проблем с toounderstand более подробно в разделе [документации LTTng](http://lttng.org/docs) и [с помощью LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
