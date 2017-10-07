---
title: "aaaOverview диагностики Azure | Документы Microsoft"
description: "Диагностику Azure можно использовать для отладки, оценки производительности, мониторинга, а также анализа трафика в облачных службах, на виртуальных машинах и в Service Fabric."
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>Что такое система диагностики Azure
Система диагностики Azure — возможность hello в Azure, которая включает hello сбор диагностических данных с развернутым приложением. Можно использовать расширения диагностики hello из нескольких разных источников. В настоящее время поддерживаются и веб-роли, и рабочие роли облачной службы Azure, и виртуальные машины Azure под управлением Microsoft Windows и Service Fabric. Другие службы Azure располагают собственной диагностикой.

## <a name="data-you-can-collect"></a>Собираемые данные
Диагностики Azure может собирать следующие типы данных hello:

| источник данных | Описание |
| --- | --- |
| Счетчики производительности |Системные и пользовательские счетчики производительности |
| Журналы приложений |Сообщения трассировки, записанные вашим приложением |
| Журналы событий Windows |Информация, передаваемая системы toohello ведение журнала событий Windows |
| Источник событий .NET |Код записи событий с помощью hello .NET [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) класса |
| Журналы IIS |Информация о веб-сайтах IIS |
| Трассировка событий Windows на основе манифестов |События трассировки событий Windows, созданные любым процессом |
| Аварийные дампы |Сведения о hello состояние процесса hello в hello событий сбоя приложения |
| Пользовательские журналы ошибок |Журналы, созданные вашим приложением или службой |
| Журналы инфраструктуры системы диагностики Azure |Информация о самой системе диагностики |

Hello расширения службы диагностики Azure можно перенести этот tooan данных учетной записи хранилища Azure или отправить его tooservices как [Application Insights](../application-insights/app-insights-cloudservices.md). Hello данные можно использовать для отладки и устранения неполадок, измерения производительности, наблюдение за использованием ресурсов, анализа трафика и планирования загрузки и аудита.

## <a name="versioning"></a>Управление версиями
См. [Журнал версий системы диагностики Microsoft Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Дальнейшие действия
Выберите службы, которые вы пытаетесь toocollect диагностики и используйте следующие статьи tooget работы hello. Используйте ссылки hello общие диагностики Azure для ссылки для выполнения конкретных задач.

## <a name="web-apps"></a>Веб-приложения
Обратите внимание на то, что в веб-приложениях диагностика Azure не используется. Поиск аналогичных сведений hello в [веб-приложений](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Облачные службы с использованием диагностики Azure
* Если с помощью Visual Studio, см. раздел [tootrace используйте Visual Studio приложения облачные службы](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget работы. В остальных случаях см. следующие статьи:
* [Как toomonitor облачной службы с помощью диагностики Azure](../cloud-services/cloud-services-how-to-monitor.md)
* [Включение системы диагностики Azure в облачных службах Azure](../cloud-services/cloud-services-dotnet-diagnostics.md)

Более подробные сведения см. в статьях:

* [Application Insights для облачных служб Azure](../application-insights/app-insights-cloudservices.md)
* [Трассировка потока hello облачные службы приложения с помощью системы диагностики Azure](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Используйте PowerShell tooset диагностики в облачных службах](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Виртуальные машины с использованием диагностики Azure
* Если с помощью Visual Studio, см. раздел [tootrace используйте Visual Studio виртуальных машинах Azure](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget работы. В остальных случаях см. следующие статьи:
* [Включение диагностики на виртуальных машинах Azure](../virtual-machines-dotnet-diagnostics.md)

Более подробные сведения см. в статьях:

* [Используйте PowerShell tooset диагностики на виртуальных машинах Azure](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Создание виртуальной машины Windows с мониторингом и диагностикой с использованием шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric с использованием диагностики Azure
Начните со статьи [Мониторинг и диагностика состояния служб в локальной среде разработки](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). В дереве навигации hello на hello осталось после передачи toothis статьи доступны многие другие статьи диагностики Service Fabric.

## <a name="general-azure-diagnostics-articles"></a>Общие статьи о диагностике Azure
* [Схема конфигурации Azure Diagnostics](https://msdn.microsoft.com/library/azure/mt634524.aspx) — Узнайте, как toochange hello toocollect файл схемы и направить данные диагностики. Обратите внимание, что можно использовать файл схемы hello toochange Visual Studio.
* [Каким образом данные диагностики Azure хранятся в хранилище Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -знать имена hello hello таблиц и больших двоичных объектов, куда будут записываться hello диагностических данных.
* Дополнительные сведения слишком[использование счетчиков производительности в Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Дополнительные сведения слишком[tooApplication сведения диагностики Azure маршрута аналитики](azure-diagnostics-configure-application-insights.md)
* Если возникнут проблемы с запуском диагностики или поиском данных в таблицах хранилища Azure, см. статью [Устранение неполадок с помощью системы диагностики Azure](azure-diagnostics-troubleshooting.md).
