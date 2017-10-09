---
title: "aaaCollect журналы с помощью диагностики Azure Linux | Документы Microsoft"
description: "В этой статье описывается, каким образом ведет журнал tooset копирование toocollect диагностики Azure из кластера Service Fabric Linux, работающих в Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Сбор журналов с помощью системы диагностики Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении. Журналы hello в центральном расположении, делает его легко tooanalyze и устранения проблем, являются ли они в ваших служб, приложений или самого кластера hello. Собирать журналы и tooupload один из способов — расширение диагностики Azure toouse hello, какие передачи журналов tooAzure хранилища, Azure Application Insights или концентраторов событий Azure. Можно также прочитать hello события из хранилища или концентраторов событий и поместить их в продукте [анализа журналов](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала. В [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) предоставляется с возможностью полного поиска по журналам и встроенной службой аналитики.

## <a name="log-sources-that-you-might-want-toocollect"></a>Вы можете toocollect источников журнала
* **Журналы Service Fabric**: создается для платформы hello через [LTTng](http://lttng.org) и отправлены tooyour учетной записи хранилища. Журналы могут быть рабочих событий или передает события среды выполнения, которые hello платформы. Эти журналы хранятся в расположении hello указывает этот манифест кластера hello. (сведения об учетной записи хранилища hello tooget, поиск hello тег **AzureTableWinFabETWQueryable** и выполните поиск **StoreConnectionString**.)
* **События приложения**. События, созданные кодом вашей службы. Вы можете использовать любое решение для ведения журналов, которое создает текстовые файлы журнала, например LTTng. Дополнительные сведения см. на трассировки приложения hello LTTng документации.  

## <a name="deploy-hello-diagnostics-extension"></a>Развертывание расширения диагностики hello
Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello. Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами. Hello действия различаются в зависимости от hello портал Azure или диспетчера ресурсов Azure.

задать toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера **диагностики** слишком**на**. После создания кластера hello, этот параметр нельзя изменить с помощью портала hello.

Затем настройте файлы hello toocollect диагностики Azure Linux (LAD) и поместите их в вашей учетной записи хранилища. Этот процесс описан в сценарии 3 («отправить файлы журнала») в статье hello [toomonitor с помощью LAD и диагностики виртуальных машин Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). После этого возвращает процесс, вы доступ toohello трассировки. Можно передать hello визуализатора tooa трассировок по своему усмотрению.

Можно также развернуть hello расширения диагностики с помощью диспетчера ресурсов Azure. Hello процесс аналогичен для Windows и Linux и задокументирован для кластеров Windows в [как toocollect журналы с диагностикой Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Также можно использовать Operations Management Suite, как описано в статье [Анализ журналов Operations Management Suite в Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

После завершения этой конфигурации агента отслеживание hello LAD hello указанные файлы журнала. Всякий раз, когда строки присоединенных toohello файл, он создает запись системного журнала, отправленных toohello хранения, указанной.

## <a name="next-steps"></a>Дальнейшие действия
какие события следует изучить при диагностике проблем с toounderstand более подробно в разделе [документации LTTng](http://lttng.org/docs) и [с помощью LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

