---
title: "Сбор журналов с помощью системы диагностики Azure | Документация Майкрософт"
description: "В этой статье описывается, как настроить систему диагностики Azure для сбора журналов из работающего в Azure кластера Service Fabric под управлением Linux."
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
ms.openlocfilehash: 3e41caaeb38c55d1c6c3bfdce2f81c86b4aff4d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Сбор журналов с помощью системы диагностики Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Во время работы кластера Azure Service Fabric рекомендуется централизованно собирать журналы со всех узлов. Если все журналы хранятся централизованно, это упрощает анализ и устранение проблем со службами, приложениями и кластером. Для отправки и сбора журналов рекомендуется использовать расширение системы диагностики Azure, которое отправляет журналы в службу хранилища Azure, Azure Application Insights или концентраторы событий Azure. Кроме того, можно считывать события из хранилища или концентраторов событий и помещать их, например, в [Log Analytics](../log-analytics/log-analytics-service-fabric.md) или другое решение для анализа журналов. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) предоставляется с возможностью полного поиска по журналам и встроенной службой аналитики.

## <a name="log-sources-that-you-might-want-to-collect"></a>Источники журналов, которые вы можете собирать
* **Журналы Service Fabric**. Создаются платформой с помощью [LTTng](http://lttng.org) и отправляются в вашу учетную запись хранения. Журналы могут включать операционные события или события среды выполнения, которые создаются платформой. Эти журналы хранятся в расположении, указанном в манифесте кластера. (Чтобы получить сведения об учетной записи хранения, выполните поиск по тегу **AzureTableWinFabETWQueryable** и найдите **StoreConnectionString**.)
* **События приложения**. События, созданные кодом вашей службы. Вы можете использовать любое решение для ведения журналов, которое создает текстовые файлы журнала, например LTTng. Дополнительные сведения см. в описании трассировки вашего приложения в документации по LTTng.  

## <a name="deploy-the-diagnostics-extension"></a>Развертывание расширения системы диагностики
Первым шагом при сборе журналов является развертывание расширения системы диагностики на каждой виртуальной машине в кластере Service Fabric. Расширение системы диагностики собирает журналы на каждой виртуальной машине и отправляет их в указанную учетную запись хранения. Действия зависят от того, что вы используете — портал Azure или Azure Resource Manager.

Чтобы развернуть расширение системы диагностики на виртуальных машинах в кластере в ходе его создания, переключите параметр **Диагностика** в состояние **Вкл**. После создания кластера изменить этот параметр на портале нельзя.

Затем в системе диагностики Azure для Linux (LAD) настройте сбор файлов и их добавление в свою учетную запись хранения. Этот процесс объясняется в разделе "Сценарий 3. Передача файлов журнала" в статье [Использование диагностического расширения Linux для мониторинга данных о состоянии и производительности виртуальных машин под управлением Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Выполнив эту процедуру, вы получите доступ к трассировкам. Трассировки можно отправлять в средство визуализации по своему усмотрению.

Кроме того, расширение системы диагностики можно развернуть с помощью Azure Resource Manager. Для Windows и Linux применяется один и тот же процесс. Он описан в документации по кластерам Windows в статье [Сбор журналов с помощью системы диагностики Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Также можно использовать Operations Management Suite, как описано в статье [Анализ журналов Operations Management Suite в Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

После завершения настройки агент LAD начнет отслеживать указанные файлы журнала. Каждый раз при добавлении новой стройки в файл он создает запись системного журнала, которая отправляется в указанное вами хранилище.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о том, какие события нужно анализировать при устранении неполадок, см. в [документации по LTTng](http://lttng.org/docs) и статье [Использование диагностического расширения Linux для мониторинга данных о состоянии и производительности виртуальных машин под управлением Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

